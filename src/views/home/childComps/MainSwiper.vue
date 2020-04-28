<template>
  <swiper class="home-swiper">
    <SwiperItem v-for="item in cbanner" :key="item.background">
      <a :href="item.link">
        <img :src="item.background" alt="">
      </a>
    </SwiperItem>

  </swiper>

</template>

<script>
  import {Swiper , SwiperItem} from "components/common/swiper";
    export default {
      name: "MainSwiper",
      props:{
        cbanner:{
          type:Array,
          default(){
            return []
          }
        }

      },
      components:{
        Swiper,
        SwiperItem
      }
    }
</script>

<style scoped>

</style>
