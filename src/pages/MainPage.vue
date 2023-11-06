<template>
  <main>
    <div class="bg-[#f5f5f5] h-auto flex flex-col sm:flex-row font-sans">
      <ImageSlider @toggleLens="toggleLens" @changeActiveImage="changeActiveImage" :lensActive="lensActive"
        :activeImage="activeImage" @getBackgroundPosition="getBackgroundPosition" @assignLeftTop="assignLeftTop" />
      <Details :left="left" :top="top" :backgroundPosition="backgroundPosition" :lensActive="lensActive"
        :activeImage="activeImage" />
    </div>
  </main>
</template>

<script>
import ImageSlider from "../components/ImageSlider.vue";
import Details from "../components/Details.vue";

export default {
  components: { ImageSlider, Details },
  data() {
    return {
      lensActive: false,
      backgroundPosition: '',
      activeImage: 0,
      left: 0,
      top: 0
    }
  },
  methods: {
    assignLeftTop([left, top]) {
      // console.log(`assign ${left} ${top}`)
      this.left = left
      this.top = top
    },
    changeActiveImage(e) {
      this.activeImage = e
    },
    getBackgroundPosition(e) {
      this.backgroundPosition = e
    },
    toggleLens() {
      this.lensActive = !this.lensActive
    }
  }
};
</script>

<style></style>
