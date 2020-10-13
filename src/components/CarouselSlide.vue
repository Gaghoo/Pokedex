<template>
    <div v-if="visibleSlide === index" class="carousel-slide">
        <slot></slot>
    </div>
</template>

<script>
export default {
    props:{
        key: Number,
        index: Number,
        visibleSlide: Number
    }
}
</script>

<style>
    
</style>