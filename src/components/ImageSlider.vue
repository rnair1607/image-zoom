<template>
    <div class="flex flex-col justify-center px-4 py-5 sm:px-40 sm:py-10 items-center h-[85vh] sm:w-[50%]">
        <div class="bg-white shadow  flex flex-col justify-around items-center h-[90%] pb-2 w-full">
            <div class="flex flex-row justify-around items-center h-[90%] w-full">
                <div class="cursor-pointer" @click="changeImage('Right')"><svg xmlns="http://www.w3.org/2000/svg"
                        fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5" />
                    </svg>
                </div>
                <div class="sm:w-[26%] sm:h-[50%] w-[70%] h-[80%] flex justify-center " @touchstart="mouseDown"
                    @touchend="mouseUp" @mouseenter="toggleLens" @mouseleave="toggleLens" @mousemove="moveLens">

                    <img :src="imageList[activeImage]" id="image" class="object-scale-down" />



                </div>
                <div class="cursor-pointer" @click="changeImage('Left')"><svg xmlns="http://www.w3.org/2000/svg" fill="none"
                        viewBox="0 0 24 24" stroke-width="2.5" stroke="#757575" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                    </svg>
                </div>
            </div>
            <div class="flex flex-row justify-around items-center w-[60%] h-[10%]">
                <div v-for="(item, index) in thumbnailList" :key="item">
                    <img :src="thumbnailList[index]" class="object-scale-down " :id="item" height="50" width="50"
                        :class="index === activeImage ? 'border-2 border-[#E53E3E]' : 'border border-gray-400'"
                        @click="changeActiveImage(index)">
                </div>
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
import thumbnail1 from "../assets/product-image-thumbnail.jpeg";
import thumbnail2 from "../assets/product-image-back-thumbnail.jpeg";
import thumbnail3 from "../assets/product-image-front-thumbnail.jpeg";

import CarousalIndicator from './CarousalIndicator.vue';

function pageOffset(el) {
    // -> {x: number, y: number}
    // get the left and top offset of a dom block element
    var rect = el.getBoundingClientRect(),
        scrollLeft = window.pageXOffset || document.documentElement.scrollLeft,
        scrollTop = window.pageYOffset || document.documentElement.scrollTop;
    return {
        y: rect.top + scrollTop,
        x: rect.left + scrollLeft
    }
}

export default {
    props: ['lensActive', 'activeImage'],
    components: {
        CarousalIndicator
    },
    data() {
        return {
            imageList: [image1, image2, image3],
            thumbnailList: [thumbnail1, thumbnail2, thumbnail3],
            imageCount: 3,
            // activeImage: 0,
            prevX: 'no',
        };
    },
    mounted() {
        // this.$emit('changeActiveImage', this.imageList[this.activeImage])
        // console.log(`activeImage: ${this.activeImage}`)
    },
    methods: {
        toggleLens() {
            // console.log('reached toggle')
            this.$emit('toggleLens')
        },
        getCursorPosition(e) {
            let a, x = 0, y = 0;
            e = e || window.event;
            let img = document.getElementById('image')

            a = img.getBoundingClientRect();

            x = e.clientX - a.left;
            y = e.clientY - a.top;

            x = x - window.scrollX;
            y = y - window.scrollY;
            // console.log(`mousex: ${x + 20} mousey:${y + 20}`)
            return { x: x, y: y };
        },
        moveLens(e) {
            // e.preventDefault();
            if (!this.lensActive) return
            var offset = pageOffset(this.$el)
            // console.log(`check from slider ${document.getElementById('zoom')}`)
            let normal = document.getElementById('image')
            let zoom = document.getElementById('zoom')
            // console.log(zoom.offsetHeight)
            // console.log(normal.offsetWidth)
            let relativeX = e.clientX - offset.x + window.scrollX
            let relativeY = e.clientY - offset.y + window.scrollY
            let normalFactorX = relativeX / normal.offsetWidth
            let normalFactorY = relativeY / normal.offsetHeight
            let x = normalFactorX * (zoom.offsetWidth * 1 - normal.offsetWidth)
            let y = normalFactorY * (zoom.offsetHeight * 1 - normal.offsetHeight)
            // zoom.style.left = -x + "px"
            // zoom.style.top = -y + "px"
            // console.log([-x, -y])
            this.$emit('assignLeftTop', [-x, -y])
            // console.log(-x, -y)
            // let pos, x, y;
            // let lens = document.getElementById("lens");
            // // let lens = document.createElement("DIV");
            // let img = document.getElementById('image')

            // // lens.setAttribute("class", "absolute border border-[#E53E3E] w-10 h-10");
            // // img.parentElement.insertBefore(lens, img);

            // pos = this.getCursorPosition(e);
            // x = pos.x - (lens.offsetWidth / 2);
            // y = pos.y - (lens.offsetHeight / 2);
            // // console.log(`X: ${x} Y:${y}`)


            // if (x > img.width - lens.offsetWidth) { x = img.width - lens.offsetWidth; }
            // if (x < 0) { x = 0; }
            // if (y > img.height - lens.offsetHeight) { y = img.height - lens.offsetHeight; }
            // if (y < 0) { y = 0; }

            // lens.style.left = (x + 20) + "px";
            // lens.style.top = y + "px";

            // this.$emit('getBackgroundPosition', [x, y])
        },
        changeActiveImage(index) {
            // let activeImage = index
            this.$emit('changeActiveImage', index)
        },
        changeImage(direction) {
            let activeImage
            // console.log('Reached: ', direction)
            if (direction === "Right") {
                if (this.activeImage === 0) return
                activeImage = this.activeImage - 1
            } else {
                if (this.activeImage === this.imageCount - 1) return
                activeImage = this.activeImage + 1

            }
            this.$emit('changeActiveImage', activeImage)
        },
        mouseDown(e) {
            e.preventDefault()
            this.prevX = e.touches[0].clientX
            // console.log('mousedown')
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

