<template>
    <div class="slide">
      <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "SwiperItem"
    }
</script>

<style scoped>
  .slide img{
    width: 100%;
  }
  .slide {
    width: 100%;
    flex-shrink: 0;
  }

</style>
