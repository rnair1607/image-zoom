<template>
    <div class="flex font-sans bg-white absolute m-4 w-[93%] sm:w-[98%] h-[97%] flex-col z-10 rounded shadow">
        <div class="flex justify-between flex-row w-full h-[5%]">
            <div class="flex flex-row h-full w-[90%]  sm:w-[95%] justify-start items-end ml-5 sm: sm:ml-10 border-b-2 ">
                <div class="ml-5 font-semibold mr-5 cursor-pointer"
                    :class="videoActive ? 'border-b-[#E53E3E] border-b-2 text-[#234B51]' : 'text-[#727C7D]'"
                    @click="toggle('video')">VIDEOS</div>
                <div class="font-semibold cursor-pointer"
                    :class="imageActive ? 'border-b-[#E53E3E] border-b-2 text-[#234B51]' : 'text-[#727C7D]'"
                    @click="toggle('image')">IMAGES</div>
            </div>
            <div class=" flex justify-end items-start flex-row h-full w-[10%] sm:w-[5%]  pt-1 pl-5" @click="togglePopup">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                    class="w-6 h-6 cursor-pointer">
                    <path fill-rule="evenodd"
                        d="M5.47 5.47a.75.75 0 011.06 0L12 10.94l5.47-5.47a.75.75 0 111.06 1.06L13.06 12l5.47 5.47a.75.75 0 11-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 01-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 010-1.06z"
                        clip-rule="evenodd" />
                </svg>

            </div>
        </div>
        <div v-if="imageActive" class="flex flex-col sm:flex-row w-full h-[95%]">
            <div
                class="flex justify-center items-center w-full h-[80%] py-5 px-0 sm:py-0 sm:px-20 sm:h-full sm:w-[80%] border">
                <div class="relative h-full w-auto overflow-hidden flex">
                    <div class="magnify fixed bg-no-repeat pointer-events-none hidden" @click="zoomout"></div>
                    <img :src="imageList[activeImage]" @click="toggleZoom" class="w-auto h-full cursor-zoom-in"
                        id="zoom-image" @touchstart="mouseDown" @touchend="mouseUp">
                </div>
            </div>

            <div class="flex justify-center items-start w-full h-[20%] sm:h-full sm:w-[20%] flex-col p-4">
                <div class="hidden sm:flex w-full h-[40%] text-justify">The standard chunk of Lorem
                    Ipsum used
                    since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from "de Finibus
                    Bonorum et Malorum" by Cicero are also reproduced in their exact original form, accompanied by English
                    versions from the 1914 translation by H. Rackham.</div>
                <div class="flex justify-evenly items-center w-full h-[60%]">
                    <div v-for="(item, index) in thumbnailList" :key="item">
                        <img :src="thumbnailList[index]" class="object-scale-down " :id="item" height="50" width="50"
                            :class="index === activeImage ? 'border-2 border-[#E53E3E]' : 'border border-gray-400'"
                            @click="changeActiveImage(index)">
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="flex w-full h-[95%] justify-center items-center font-bold">No videos to preview</div>
    </div>
</template>

<script>
import image1 from '../assets/product-image-large.jpeg'
import image2 from '../assets/product-image-back-large.jpeg'
import image3 from '../assets/product-image-front-large.jpeg'
import thumbnail1 from "../assets/product-image-thumbnail.jpeg";
import thumbnail2 from "../assets/product-image-back-thumbnail.jpeg";
import thumbnail3 from "../assets/product-image-front-thumbnail.jpeg";

export default {
    data() {
        return {
            imageList: [image1, image2, image3],
            thumbnailList: [thumbnail1, thumbnail2, thumbnail3],
            imageActive: true,
            videoActive: false,
            activeImage: 0,
            zoomed: false,
            zoomImage: 'no',
            magnifyingGlass: 'no',
            imageCount: 3,
            prevX: 'no',
        }
    },
    mounted() {
        this.zoomImage = document.getElementById('zoom-image');
        this.magnifyingGlass = document.querySelector('.magnify');
    },
    methods: {
        changeActiveImage(index) {
            this.activeImage = index
        },
        changeImage(direction) {
            let activeImage
            if (direction === "Right") {
                if (this.activeImage === 0) return
                activeImage = this.activeImage - 1
            } else {
                if (this.activeImage === this.imageCount - 1) return
                activeImage = this.activeImage + 1

            }
            this.activeImage = activeImage
        },
        mouseDown(e) {
            this.prevX = e.touches[0].clientX
        },
        mouseUp(e) {
            if (this.prevX < e.changedTouches[0].clientX) {
                if ((e.changedTouches[0].clientX - this.prevX) < 100) return

                this.changeImage("Right")

            } else {
                if ((this.prevX - e.changedTouches[0].clientX) < 100) return
                this.changeImage("Left")

            }

            this.prevX = 'no'
            e.stopPropagation()
        },

        zoomout(e) {
            if (this.zoomed) {
                this.magnifyingGlass.style.display = 'none';
            }
        },
        toggleZoom(e) {
            if (this.zoomed) {
                this.magnifyingGlass.style.display = 'none';
                this.zoomed = false
            } else {
                let zoomFactor = 1.5;
                let offsetX = e.clientX - this.zoomImage.getBoundingClientRect().left;
                let offsetY = e.clientY - this.zoomImage.getBoundingClientRect().top;
                let backgroundPositionX = -offsetX * zoomFactor + 'px';
                let backgroundPositionY = -offsetY * zoomFactor + 'px';

                this.magnifyingGlass.style.backgroundImage = `url(${this.imageList[this.activeImage]})`;
                this.magnifyingGlass.style.display = 'block';
                this.magnifyingGlass.style.backgroundPosition = `${backgroundPositionX} ${backgroundPositionY}`;
                // this.magnifyingGlass.style.left = e.clientX + 10 + 'px';
                // this.magnifyingGlass.style.top = e.clientY - this.magnifyingGlass.clientHeight / 2 + 'px';
                this.magnifyingGlass.style.cursor = 'zoom-out'
                this.magnifyingGlass.style.height = this.zoomImage.height + 'px'
                this.magnifyingGlass.style.width = this.zoomImage.width + 'px'

                this.zoomed = true
            }
        },
        toggle(s) {
            if (s === 'image') {
                this.imageActive = true
                this.videoActive = false
            } else {
                this.imageActive = false
                this.videoActive = true
            }
        },
        togglePopup() {
            this.$emit('togglePopup')
        }
    }

}
</script>

<style></style>