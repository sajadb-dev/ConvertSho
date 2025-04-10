<script lang="ts">
    let {target = '', text = '', path = "", classnames = '', arialabel} = $props();
</script>

<li class="animated-background {classnames} my-auto flex text-black dark:text-white hover:drop-shadow-lg bg-gradient-to-r hover:from-pink-500 hover:to-orange-500 hover:text-transparent hover:bg-clip-text">
    <a href={path} aria-label={arialabel} {target} class="w-full h-full">{text}</a>
</li>