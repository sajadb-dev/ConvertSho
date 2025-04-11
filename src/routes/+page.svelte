<script lang="ts">
	import Fileitem from "$lib/components/Fileitem.svelte";
  import { FileUpload } from "melt/builders";
	import { SvelteSet } from "svelte/reactivity";
  import UploadIcon from "~icons/tabler/cloud-upload";
  import XIcon from "~icons/tabler/x";


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
    const accepted_files = {
    "image/*": [
      ".jpg",
      ".jpeg",
      ".png",
      ".gif",
      ".bmp",
      ".webp",
      ".ico",
      ".tif",
      ".tiff",
      ".raw",
      ".tga",
    ],
    "audio/*": [],
    "video/*": [],
  };

  const fileUpload = new FileUpload({
  accept: 'image/*,video/*,audio/*',
  multiple: true
  });

  let files = $derived.by(() => {
		if (fileUpload.selected instanceof SvelteSet) {
			return Array.from(fileUpload.selected);
		}
		return [fileUpload.selected].filter((f): f is File => !!f);
	});

  $inspect(files);
</script>
<div class="py-28 lg:py-44 flex flex-col lg:flex-row">
  <div class="w-full lg:w-2/6 mb-12 flex items-center justify-center">
    <div class="w-full h-0 lg:w-1/3 lg:h-full"></div>
  </div>
  <div class="w-full">
    <div class="w-full px-2 flex flex-col text-center gap-8">
        <h1 class="text-4xl lg:text-6xl">فایل هاتو تبدیل کن</h1>
        <h3 class="text-2xl lg:text-4xl">فایل های صوتی تصویری خود را به آسانی به فرمت های مختلف تبدیل کنید</h3>
    </div>
    <div class="h-96 mt-20 flex justify-center">
      {#if files.length === 0}
      <div id="dropzone" class="w-10/12">
        <input {...fileUpload.input}/>
        <div class="relative flex w-full h-full cursor-pointer
				  flex-col items-center justify-center gap-4
				  rounded-xl border-2 border-dashed border-gray-300 bg-slate-100
				  p-6 text-center transition-colors
				  hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700" 
          class:!border-accent-500={fileUpload.isDragging} 
          {...fileUpload.dropzone}>
          {#if fileUpload.isDragging}
          <p class="text-accent-400 font-medium">Drop files here</p>
          {:else}
            <UploadIcon class="text-4xl" />
					  <p class="text-md text-gray-500 dark:text-gray-400">
						  <span class="font-semibold text-gray-900 dark:text-white">Click to upload</span>
						  or drag and drop
					  </p>
          {/if}
        </div>
    </div>
    {:else}
    <div class=" w-full h-full flex flex-col gap-8 items-center">
      {#each files as file }
      <Fileitem title = {file.name} filetype = {file.type}/>
      {/each}
    </div>
    {/if}
    </div>
  </div>
  <div class="w-full lg:w-2/6 flex items-center justify-center">
    <div class="w-full h-28 lg:w-1/3 lg:h-full"></div>
  </div>
</div>