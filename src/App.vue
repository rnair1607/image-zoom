<template>
  <div>
    <NavBar />
    <main>
      <div class="bg-[#f5f5f5] h-auto flex flex-col sm:flex-row">
        <div class="border-2 border-red-500 h-[85vh] w-full sm:w-[50%]"></div>
        <div class="border-2 border-sky-500 h-[85vh] w-full sm:w-[50%]"></div>
      </div>
    </main>
  </div>
</template>

<script setup>
import NavBar from "./components/NavBar.vue";
</script>
