<template>
  <nav class="relative flex w-full flex-wrap items-center justify-between py-2 border-b-2 h-[15vh]">
    <div class="flex w-full flex-wrap items-center justify-between px-3">
      <div class="ml-[2vw] sm:ml-[10vw] logo">
        <a href="">
          <img :src="logo" class="w-[60%]" />
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

<style></style>
