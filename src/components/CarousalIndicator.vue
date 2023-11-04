<template>
    <div @click="changeActive" class="rounded-full h-2 w-2 cursor-pointer"
        :class="active ? 'bg-[#E53E3E]' : 'bg-[#BDBDBD]'"></div>
</template>

<script>
export default {
    props: ['active'],
    methods: {
        changeActive() {
            this.$emit('activate')
        }
    }

}
</script>

<style></style>