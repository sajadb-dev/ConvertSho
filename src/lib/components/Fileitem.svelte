<script lang="ts">
    import MovieIcon from "~icons/tabler/movie";
    import AudioIcon from "~icons/tabler/volume";
    import ImageIcon from "~icons/tabler/photo";
    import XIcon from "~icons/tabler/x";
    import * as Select from "$lib/components/ui/select/index.js";
    import * as Tabs from "$lib/components/ui/tabs/index.js";
	import Button from "./ui/button/button.svelte";

    let { filetype, title, removeitem} = $props();

    const extensions = {
      image: [
        "jpg",
        "jpeg",
        "png",
        "gif",
        "bmp",
        "webp",
        "ico",
        "tif",
        "tiff",
        "svg",
        "raw",
        "tga",
      ],
      video: [
        "mp4",
        "m4v",
        "mp4v",
        "3gp",
        "3g2",
        "avi",
        "mov",
        "wmv",
        "mkv",
        "flv",
        "ogv",
        "webm",
        "h264",
        "264",
        "hevc",
        "265",
      ],
      audio: ["mp3", "wav", "ogg", "aac", "wma", "flac", "m4a"],
    };
    let value = $state("");
    const defaultValues = "video";
    let triggerContent = $derived.by(() => {
        if(value !== "") {
            if(filetype.includes('image'))
                return extensions.image.find((f) => f === value)
            else if(filetype.includes('video'))
                return extensions.video.find((f) => f === value)
            else if(filetype.includes('audio'))
                return extensions.audio.find((f) => f === value)
        }
        else
        return "فرمت"

    });

</script>

<div class="w-full min-h-20 px-2 lg:px-12 flex gap-2 lg:gap-6 items-center justify-between rounded-lg border bg-zinc-50 border-slate-300 drop-shadow-md">
    <div class="flex gap-2 lg:gap-6 items-center">
        {#if filetype.includes('video')}
            <MovieIcon class="text-4xl text-amber-500" />
        {:else if filetype.includes('audio')}
            <AudioIcon class="text-4xl text-blue-500" />
        {:else if filetype.includes('image')}
            <ImageIcon class="text-4xl text-purple-500" />
        {/if}
        <div class="flex gap-1">
            <span class="w-8">نام :</span>
            <span class="max-w-[12ch] sm:max-w-[20ch] md:max-w-[40ch] lg:max-w-[60ch] font-sans truncate">{title}</span>
        </div>
    </div>
    <div class="flex gap-2 lg:gap-8 font-mono">
    <Select.Root type="single" bind:value>
        <Select.Trigger class="w-32 outline-none focus:outline-none focus:ring-0 text-center text-muted-foreground bg-background text-md font-medium">
            {triggerContent}
        </Select.Trigger>
        <Select.Content class="h-fit">
            {#if filetype.includes("image")}
                <div class="grid grid-cols-2 gap-2 w-fit">
                    {#each extensions.image as elm}
                        <div class="col-span-1 text-center">
                            <Select.Item value={elm} label={elm} class="mx-auto font-mono">
                                {elm}
                            </Select.Item>
                        </div>
                    {/each}
                </div>
            {/if}
            {#if filetype.includes("video")}
                <Tabs.Root value={defaultValues} class="w-full">
                    <Tabs.List class="w-full">
                        <Tabs.Trigger value="video" class="w-full">
                            Video
                        </Tabs.Trigger>
                        <Tabs.Trigger value="audio" class="w-full">
                            Audio
                        </Tabs.Trigger>
                    </Tabs.List>
                    <Tabs.Content value="video">
                        <div class="grid grid-cols-3 gap-2 w-fit">
                            {#each extensions.video as elm}
                                <div class="col-span-1 text-center">
                                    <Select.Item value={elm} label={elm} class="mx-auto font-mono">
                                        {elm}
                                    </Select.Item>
                                </div>
                            {/each}
                        </div>
                    </Tabs.Content>
                    <Tabs.Content value="audio">
                        <div class="grid grid-cols-3 gap-2 w-fit">
                            {#each extensions.audio as elm}
                                <div class="col-span-1 text-center">
                                    <Select.Item value={elm} label={elm} class="mx-auto font-mono">
                                        {elm}
                                    </Select.Item>
                                </div>
                            {/each}
                        </div>
                    </Tabs.Content>
                </Tabs.Root>
            {/if}
            {#if filetype.includes("audio")}
                <div class="grid grid-cols-2 gap-2 w-fit">
                    {#each extensions.audio as elm}
                        <div class="col-span-1 text-center">
                            <Select.Item value={elm} label={elm} class="mx-auto font-mono">
                                {elm}
                            </Select.Item>
                        </div>
                    {/each}
                </div>
            {/if}
        </Select.Content>
    </Select.Root>
    <Button variant="outline" size="icon" onclick={removeitem}><XIcon/></Button>
    </div>
</div>