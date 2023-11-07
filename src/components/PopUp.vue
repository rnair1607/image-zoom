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
                <svg xmlns=" http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                    class="w-6 h-6 cursor-pointer">
                    <path fill-rule="evenodd"
                        d="M5.47 5.47a.75.75 0 011.06 0L12 10.94l5.47-5.47a.75.75 0 111.06 1.06L13.06 12l5.47 5.47a.75.75 0 11-1.06 1.06L12 13.06l-5.47 5.47a.75.75 0 01-1.06-1.06L10.94 12 5.47 6.53a.75.75 0 010-1.06z"
                        clip-rule="evenodd" />
                </svg>

            </div>
        </div>
        <div class=" w-full h-[95%]"></div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            imageActive: true,
            videoActive: false
        }
    },
    methods: {
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