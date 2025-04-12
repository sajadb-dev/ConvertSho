<script lang="ts" module>
    // Define your toast data.
    type ToastData = {
      title: string;
      description: string;
    };
  
    const toaster = new Toaster<ToastData>({
        closeDelay: 20000,
    }
    );
  
    export const addToast = toaster.addToast;
  </script>
  
  <script lang="ts">
    import { Toaster } from "melt/builders";
    import { fly } from "svelte/transition";
    import XIcon from "~icons/tabler/x";
  </script>
  
  <div {...toaster.root}
    class="fixed !bottom-4 !right-4 flex w-[300px] flex-col">
    {#each toaster.toasts as toast, i (toast.id)}
      <div {...toast.content}
        class="relative flex h-[--toast-height] w-full items-center justify-between rounded-xl border bg-white px-4 text-left transition dark:bg-gray-800"
        class:text-red-500={toast.data.title === "Error" || "خطا"}
        class:border-red-200={toast.data.title === "Error" || "خطا"}
        class:text-green-500={toast.data.title === "Success" || "موفقیت"}
        class:border-green-200={toast.data.title === "Success" || "موفقیت"}
        class:text-yellow-500={toast.data.title === "Warning" || "اخطار"}
        class:border-yellow-200={toast.data.title === "Warning" || "اخطار"}
        style:--n={toaster.toasts.length - i}
			in:fly={{ y: 60, opacity: 0.9 }}
			out:fly={{ y: 20 }}>
        <div>
            <h3 {...toast.title} dir="rtl" class="whitespace-nowrap text-sm font-bold font-sans">
                {toast.data.title}
            </h3>
            <div {...toast.description} dir="rtl" class="text-xs font-sans text-gray-700 dark:text-gray-300">
                {toast.data.description}
            </div>
        </div>
        <button {...toast.close} 
            class="bg-transparent text-gray-300 hover:text-gray-400 dark:hover:text-gray-100" 
            aria-label="dismiss alert">
            <XIcon/>
        </button>
      </div>
    {/each}
  </div>

  <style>
	:global([popover]) {
		inset: unset;
	}

	[data-melt-toaster-root] {
		--gap: 0.75rem;
		--hover-offset: 1rem;
		--toast-height: 4rem;
		--hidden-offset: 0.75rem;

		--hidden-toasts: calc(var(--toasts) - 1);

		overflow: visible;
		display: grid;
		grid-template-rows: var(--toast-height) repeat(var(--hidden-toasts), var(--hidden-offset));
		grid-template-columns: 1fr;
		gap: 0;
		background: unset;
		padding: 0;
	}

	[data-melt-toaster-root]:hover {
		grid-template-rows: var(--hidden-offset) var(--toast-height) repeat(
				var(--hidden-toasts),
				calc(var(--toast-height) + var(--gap))
			);
	}

	[data-melt-toaster-toast-content] {
		position: absolute;
		pointer-events: auto;
		bottom: 0;
		left: 0;
		box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);

		transform-origin: 50% 0%;
		transition: all 350ms ease;
	}

	:global([data-theme="dark"] [data-melt-toaster-toast-content]) {
		box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.5);
	}

	[data-melt-toaster-toast-content]:nth-last-child(n + 4) {
		z-index: 1;
		scale: 0.925;
		opacity: 0;
		translate: 0 calc(-3 * var(--hidden-offset));
	}

	[data-melt-toaster-toast-content]:nth-last-child(-n + 3) {
		z-index: 2;
		scale: 0.95;
		translate: 0 calc(-2 * var(--hidden-offset));
	}

	[data-melt-toaster-toast-content]:nth-last-child(-n + 2) {
		z-index: 3;
		scale: 0.975;
		translate: 0 calc(-1 * var(--hidden-offset));
	}

	[data-melt-toaster-toast-content]:nth-last-child(-n + 1) {
		z-index: 4;
		scale: 1;
		translate: 0;
	}

	[data-melt-toaster-root]:hover [data-melt-toaster-toast-content] {
		scale: 1;
		opacity: 1;
		--toast-gap: calc(calc(var(--gap) * var(--n)) + var(--hover-offset));
		--percentage: calc(-100% * calc(var(--n) - 1));
		translate: 0 calc(var(--percentage) - var(--toast-gap));
	}
</style>