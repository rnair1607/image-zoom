<template>
  <div class="h-[85vh] w-full sm:w-[50%] px-5 sm:px-20 py-10" v-if="!lensActive">
    <div class="flex flex-row justify-between w-full h-auto py-2 text-base font-sans">
      <div class="text-[#A9A9A9]">SAMSUNG</div>
      <div class="text-[#398B61]">Hurry Limited Stock</div>
    </div>
    <div class="flex flex-col item-start w-full h-auto py-2 text-[#282827] font-sans border-b-4">
      <div class="mb-4 font-bold text-xl">Samsung Galaxy S23 Plus 5G</div>
      <div class="pb-4 border-b-4 font-bold text-xl">£880.00</div>
      <div class="flex flex-row py-3 text-base">
        <div class="font-semibold mr-2">Sim:</div>
        DUAL SIM
      </div>
      <div class="flex flex-row py-3 text-base">
        <div class="font-semibold mr-2">Condition:</div>
        LIKE NEW
      </div>
      <div class="flex flex-row py-3 text-base">
        <div class="font-semibold mr-2">Colour:</div>
        LAVENDER
      </div>
      <div class="flex flex-row py-3 text-base">
        <div class="font-semibold mr-2">Network:</div>
        UNLOCKED
      </div>
      <div class="flex flex-row py-3 text-base">
        <div class="font-semibold mr-2">Storage:</div>
        512GB
      </div>
    </div>
    <div class="quantity flex flex-row w-full h-auto py-5 items-center justify-center sm:justify-start">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575"
        class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 12h-15" />
      </svg>
      <div class="bg-[#EEEEEE] h-8 w-8 mx-2 flex justify-center items-center text-[#265986]">
        1
      </div>
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575"
        class="w-6 h-6">
        <path strokeLinecap="round" strokeLinejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
      </svg>
    </div>
    <div class="flex w-full h-auto pt-2">
      <button class="bg-[#FFD812] p-4 w-full rounded font-semibold">
        Add to Basket
      </button>
    </div>
  </div>
  <div class="h-[85vh] w-full sm:w-[50%] px-5 sm:px-20 py-10 flex justify-center relative" id="zoomedImg" v-else>
    <div class=" w-[80%] h-[80%] overflow-hidden relative">
      <img :src="imageList[activeImage]" id="zoom" ref="zoom" class="absolute max-w-[200%] h-[200%] "
        :style="{ 'left': localLeft, 'top': localTop }">
    </div>
  </div>
</template>

<script>
import zoomed1 from "../assets/product-image-large.jpeg";
import zoomed2 from "../assets/product-image-back-large.jpeg";
import zoomed3 from "../assets/product-image-front-large.jpeg";

export default {
  props: [
    'backgroundPosition',
    'lensActive',
    'activeImage',
    'top',
    'left'
  ],
  data() {
    return {
      imageList: [zoomed1, zoomed2, zoomed3],
      localLeft: '0px',
      localTop: '0px'
    }
  },
  mounted() {
    this.localLeft = this.left
    this.localTop = this.top
  },
  watch: {
    left: function (newVal) {
      this.localLeft = `${(newVal / 3.2) + 500}px`
    },
    top: function (newVal) {
      this.localTop = `${(newVal / 1.5) + 310}px`
    },
  }

};
</script>

<style scoped>
svg {
  cursor: pointer;
}
</style>
