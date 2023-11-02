<template>
  <nav
    class="relative flex w-full flex-wrap items-center justify-between bg-[#FBFBFB] py-2 text-neutral-500 shadow-lg hover:text-neutral-700 focus:text-neutral-700 dark:bg-neutral-600 lg:py-4"
  >
    <div class="flex w-full flex-wrap items-center justify-between px-3">
      <div class="ml-2 logo">
        <a href="">
          <img :src="logo" />
        </a>
      </div>
    </div>
  </nav>
</template>
<script>
import logo from "../assets/tbps-logo.webp";

export default {
  data() {
    return {
      logo: logo,
    };
  },
};
</script>
