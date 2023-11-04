<template>
  <main>
    <div class="bg-[#f5f5f5] h-auto flex flex-col sm:flex-row font-sans">
      <ImageSlider />
      <Details />
    </div>
  </main>
</template>

<script>
import ImageSlider from "../components/ImageSlider.vue";
import Details from "../components/Details.vue";

export default { components: { ImageSlider, Details } };
</script>

<style></style>
