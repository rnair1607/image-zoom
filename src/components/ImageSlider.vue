<template>
    <div class="flex flex-col justify-center px-4 py-5 sm:px-40 sm:py-10 items-center h-[85vh] sm:w-[50%]">
        <div class="bg-white shadow  flex justify-around items-center h-[90%] pb-2 w-full">
            <div class="cursor-pointer" @click="changeImage('Right')"><svg xmlns="http://www.w3.org/2000/svg" fill="none"
                    viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
                </svg>
            </div>
            <div class="sm:w-[50%] sm:h-[50%] w-[70%] h-[80%] flex justify-center" @touchstart="mouseDown"
                @touchend="mouseUp">
                <img :src="imageList[activeImage]" class="object-scale-down" />
            </div>
            <div class="cursor-pointer" @click="changeImage('Left')"><svg xmlns="http://www.w3.org/2000/svg" fill="none"
                    viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                </svg>
            </div>
        </div>
        <div class="flex flex-row justify-center items-center h-[10%] w-full">
            <div class="flex flex-row justify-evenly items-center h-full w-[15%]">
                <div v-for="(item, index) in imageList" :key="item">
                    <CarousalIndicator :active="index === activeImage" @activate="changeActiveImage(index)" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import image1 from "../assets/product-image.jpeg";
import image2 from "../assets/product-image-back.jpeg";
import image3 from "../assets/product-image-front.jpeg";

import CarousalIndicator from './CarousalIndicator.vue';

export default {
    components: {
        CarousalIndicator
    },
    data() {
        return {
            imageList: [image1, image2, image3],
            imageCount: 3,
            activeImage: 0,
            prevX: 'no'
        };
    },
    methods: {
        changeActiveImage(index) {
            this.activeImage = index
        },
        changeImage(direction) {
            console.log('Reached: ', direction)
            if (direction === "Right") {
                if (this.activeImage === 0) return
                this.activeImage -= 1
            } else {
                if (this.activeImage === this.imageCount - 1) return
                this.activeImage += 1
            }
        },
        mouseDown(e) {
            e.preventDefault()
            this.prevX = e.touches[0].clientX
            console.log('mousedown')
        },
        mouseUp(e) {
            console.log(e)
            if (this.prevX < e.changedTouches[0].clientX) {
                if ((e.changedTouches[0].clientX - this.prevX) < 100) return

                this.changeImage("Right")

            } else {
                if ((this.prevX - e.changedTouches[0].clientX) < 100) return
                this.changeImage("Left")

            }
            this.prevX = 'no'
            e.stopPropagation()
        }
    },
};
</script>

