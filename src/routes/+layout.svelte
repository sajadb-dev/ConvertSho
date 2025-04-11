<script lang="ts">
	import '../app.css';
	import Navelement from '$lib/components/navelement.svelte';
	import MenuList from '$lib/components/MenuList.svelte';
	import CloseIcon from '../lib/components/CloseIcon.svelte';
	import { page } from '$app/state';
  	import { base } from '$app/paths';
	import AppIcon from '$lib/components/AppIcon.svelte';

	let { children } = $props();

	let menuicon = $state();
	let closeicon = $state();
	let navbar = $state();

	const pageUrl = $derived(() => page.url);

	function onclick() {
    	if (menuicon) menuicon.classList.toggle('hidden');
    	if (closeicon) closeicon.classList.toggle('hidden');
    	if (navbar) navbar.classList.toggle('h-14');
	}
	$effect(() => {
    if (pageUrl()) {
		if (navbar) 
			if(!navbar.classList.contains('h-14')) onclick();
    }
  });
</script>


<nav class="h-14 w-9/12 fixed container px-1 lg:px-2 mt-6 center rounded-lg border border-slate-300 drop-shadow-md backdrop-blur-2xl z-30 hidden md:inline">
	<div class="mx-4 lg:mx-12 h-full flex flex-row justify-between">
		<div class="my-auto flex flex-row justify-center text-center items-center font-base text-md">
			<div class=" bg-rose-600 px-4 py-2 rounded-md hover:bg-opacity-85 text-white"><a class="flex items-center gap-2" href="{base}/app-download"><AppIcon/>دانلود اپلیکیشن</a></div>
		</div>
		<ul class="h-full my-auto flex flex-row gap-[5vw] lg:gap-[6vw] font-base text-md">
			<Navelement path="{base}/privacy" text="حریم خصوصی" arialabel="Go To Privacy Page"/>
			<Navelement path="{base}/about" text="درباره" arialabel="Go To About Page"/>
			<Navelement path="{base}/" text="خانه" arialabel="Go To Home Page"/>
		</ul>
		<div class="h-full"><a href="{base}/" aria-label="Go Back To Home Page" class="w-full h-full flex align-text-bottom items-center font-bold text-2xl text-amber-500 font-ghasem">تبدیل شو</a></div>
	</div>
</nav>
<nav bind:this={navbar} id="mobile-nav" class="top-4 left-4 w-[90dvw] h-14 overflow-hidden fixed center rounded-lg border border-slate-400 drop-shadow-2xl font-paper backdrop-blur-2xl z-30 md:hidden">
    <div class=" w-full h-14 mx-2 px-4 flex flex-row justify-between items-center relative">
		<div class="h-full"><a href="/" class="w-full h-full flex items-center text-2xl text-amber-500 font-ghasem">تبدیل شو</a></div>
		<ul class="flex justify-center items-center gap-6">
			<li class="h-8 ml-3">
				<button type="button" aria-label="hamburgermenu" class="w-8 h-full" {onclick}>
					<div class="" bind:this={menuicon}>
						<MenuList  classnames="w-full h-full cursor-pointer fill-black dark:fill-white"/>
					</div>
					<div class="hidden" bind:this={closeicon}>
						<CloseIcon classnames="w-full h-full cursor-pointer fill-black dark:fill-white"/>
					</div>
				</button>
			</li>
	</div>
	<div>
		<div class="mx-6 my-6 h-full flex flex-row justify-between">
			<ul class="h-full my-auto flex flex-col gap-[6vw] font-base text-lg">
				<Navelement path="{base}/" text="خانه" arialabel="Go To Home Page"/>
				<Navelement path="{base}/about" text="درباره" arialabel="Go To About Page"/>
				<Navelement path="{base}/privacy" text="حریم خصوصی" arialabel="Go To Privacy Page"/>
				<Navelement path="{base}/app-download" text="دانلود اپلیکیشن" arialabel="Go To Application Download Page" classnames="text-lg text-orange-600 dark:text-orange-400 font-bold "/>
			</ul>
		</div>
	</div>
</nav>

{@render children()}

<div class="w-full h-20 fixed bottom-0"></div>
<footer class="w-full h-40 bg-slate-400 border-t border-zinc-700">

</footer>
