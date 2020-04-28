<template>
  <div id="home">
    <nav-bar class="home-nav-bar">
      <div slot="center" >购物街</div>
    </nav-bar>
    <main-swiper :cbanner="banner"/>

  </div>

</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
  import MainSwiper from "./childComps/MainSwiper";
  export default {
    name: "Home",
    data(){
      return{
        banner:[
          {
            link:'http://www.baidu.com',
            background:'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3757720535,2190197971&fm=26&gp=0.jpg'
          },
          {
            link:'http://www.baidu.com',
            background:'https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=3957723262,1525538132&fm=26&gp=0.jpg'
          }
        ]
      }
    },
    components:{
      NavBar,
      MainSwiper
    }
  }
</script>

<style scoped>
  .home-nav-bar{
    color: white;
    background-color: #F78097;
  }


</style>
