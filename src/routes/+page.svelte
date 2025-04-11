<script lang="ts">
import Dropzone from "svelte-file-dropzone";

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

  const files = {
        accepted: [] as File[],
        rejected: [] as File[],
    };

    function handleFilesSelect(e) {
        let { acceptedFiles, fileRejections } = e.detail;
        files.accepted = [...files.accepted, ...acceptedFiles];
        files.rejected = [...files.rejected, ...fileRejections];
    }

    $inspect(files.accepted);
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
      <div id="dropzone" class="w-10/12">
        <Dropzone 
          name="File Selector"
          containerClasses="h-full flex items-center justify-center text-center" 
          accept="image/*,audio/*,video/*"
          multiple = {true}
          on:drop={handleFilesSelect}
          />
    </div>
    </div>
  </div>
  <div class="w-full lg:w-2/6 flex items-center justify-center">
    <div class="w-full h-28 lg:w-1/3 lg:h-full"></div>
  </div>
</div>