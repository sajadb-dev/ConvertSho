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

    function handleFilesSelect(e: CustomEvent<{ acceptedFiles: File[]; fileRejections: File[] }>) {
        const { acceptedFiles, fileRejections } = e.detail;
        files.accepted = [...files.accepted, ...acceptedFiles];
        files.rejected = [...files.rejected, ...fileRejections];
    }
</script>
<div class="w-full pt-36 px-2 lg:pt-44 flex flex-col text-center gap-8">
    <h1 class="text-4xl lg:text-6xl">فایل هاتو تبدیل کن</h1>
    <h3 class="text-2xl lg:text-4xl">فایل های صوتی تصویری خود را به آسانی به فرمت های مختلف تبدیل کنید</h3>
</div>
<div class="h-full mt-12 flex justify-center">
    <div class="w-8/12 h-96">
        <Dropzone class="h-full flex items-center justify-center text-center bg-slate-300 rounded-lg border-4 border-zinc-400 border-dashed" accept="image/*,audio/*,video/*" ondrop={handleFilesSelect}></Dropzone>
    </div>
</div>
