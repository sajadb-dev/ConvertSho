<script lang="ts">
    import { Button } from "$lib/components/ui/button/index.js";
    import GithubLogo from "~icons/tabler/brand-github";
</script>

<div class="min-h-[100dvh] px-4 lg:px-60 py-32 lg:py-48 space-y-12 text-md md:text-lg pb-4 md:pb-8 font-sans">
    <div class="w-full flex justify-center text-4xl font-bold font-arsoo">دانلود اپلیکیشن</div>
    <p dir="rtl" class="mb-6 text-lg">
        نسخه دسکتاپ یا موبایل این ابزار را دانلود کنید و به راحتی فایل‌های صوتی و تصویری خود را به فرمت‌های مختلف تبدیل کنید — سریع، ایمن و کاملاً آفلاین.
      </p>
    
      <h3 dir="rtl" class="text-xl font-semibold mb-3">ویژگی‌ها:</h3>
      <ul dir="rtl" class="list-disc pr-6 space-y-2 text-base">
        <li>تبدیل سریع فایل‌های صوتی و تصویری با استفاده از FFmpeg</li>
        <li>اجرا به‌صورت کاملاً محلی بدون نیاز به اینترنت</li>
        <li>رابط کاربری ساده و کاربرپسند</li>
        <li>بدون محدودیت حجم فایل</li>
      </ul>
    
      <div class="mt-8 flex flex-col gap-4 items-center justify-center">
        <p class="text-xl font-semibold mb-3">به زودی</p>
        <Button disabled={true}>
            <GithubLogo/>
            <span>دریافت از گیت‌هاب</span>
        </Button>
      </div>
</div>