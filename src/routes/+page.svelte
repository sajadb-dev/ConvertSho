<script lang="ts">
	import Fileitem from "$lib/components/Fileitem.svelte";
  import { FileUpload } from "melt/builders";
	import { SvelteSet } from "svelte/reactivity";
  import { Button } from "$lib/components/ui/button/index.js";
  import { addToast } from '$lib/components/Toaster.svelte'
  import UploadIcon from "~icons/tabler/cloud-upload";
  import ConvertIcon from "~icons/simple-icons/convertio"


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

  let errorMsg = $state();

  const fileUpload = new FileUpload({
    accept: 'image/*,video/*,audio/*',
    multiple: true,
    maxSize: 2147483648,
    onError(error) {
      addToast({
      data: {
        title: 'اخطار',
        description: toastMsg(error.message)
        }
      })
    },
  });

  let files = $derived.by(() => {
		if (fileUpload.selected instanceof SvelteSet) {
			return Array.from(fileUpload.selected);
		}
		return [fileUpload.selected].filter((f): f is File => !!f);
	});

  function toastMsg(a: string) {
    if(a.includes("File type application/postscript is not accepted"))
    return "فرمت فایل انتخابی اشتباه"
  if(a.includes("exceeds maximum size"))
    return "حجم فایل انتخابی بیشتر از سقف مجاز"
  else
    return "خطا در پروسه تبدیل"
  }

</script>
<div class="pt-28 lg:pt-44 flex flex-col lg:flex-row">
  <div class="w-full lg:w-2/6 mb-12 flex items-center justify-center">
    <div class="w-full h-0 lg:w-1/3 lg:h-full"></div>
  </div>
  <div class="w-full">
    <div class="w-full px-2 flex flex-col text-center gap-8">
        <h1 class="text-4xl lg:text-6xl">فایل هاتو تبدیل کن</h1>
        <h3 class="text-2xl lg:text-4xl">فایل های صوتی تصویری خود را به آسانی به فرمت های مختلف تبدیل کنید</h3>
    </div>
    <div class="mt-20 flex justify-center">
      {#if files.length === 0}
      <div id="dropzone" class="w-10/12 h-96">
        <input {...fileUpload.input}/>
        <div class="relative flex w-full h-full cursor-pointer
				  flex-col items-center justify-center gap-4
				  rounded-xl border-2 border-dashed border-gray-300 bg-slate-100
				  p-6 text-center transition-colors
				  hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700" 
          class:!border-accent-500={fileUpload.isDragging} 
          {...fileUpload.dropzone}>
          {#if fileUpload.isDragging}
          <p dir="rtl" class="text-accent-400 font-medium">بنداز همین جا</p>
          {:else}
            <UploadIcon class="text-4xl" />
					  <p dir="rtl" class="text-md text-gray-500 dark:text-gray-400">
						  <span class="font-semibold text-gray-900 dark:text-white">برای آپلود کلیک کنید</span>
						  یا فایل خود را اینجا بی اندازید
					  </p>
            <p dir="rtl">( سقف مجاز فایل 2GB )</p>
          {/if}
        </div>
    </div>
    {:else}
    <div class=" w-full mx-2 flex flex-col gap-8 items-center">
      {#each files as file }
      <Fileitem title = {file.name} filetype = {file.type} removeitem={() => {fileUpload.remove(file);}}/>
      {/each}
      <div class="w-full flex justify-end">
        <Button class="w-40 flex gap-2" onclick={() => console.log('ff')} disabled>
          <ConvertIcon/>
          <p>تبدیل</p>
        </Button>
      </div>
    </div>
    {/if}
    </div>
  </div>
  <div class="w-full lg:w-2/6 flex items-center justify-center">
    <div class="w-full h-28 lg:w-1/3 lg:h-full"></div>
  </div>
</div>