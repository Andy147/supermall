<template>
  <div id="ad-swiper">
    <div class="swiper" @touchstart="touchStart" @touchmove="touchmove" @touchend="touchend">
      <slot></slot></div>

  </div>

</template>

<script>
    export default {
      name: "Swiper",
      data(){
        return{
          totalWidth:0,//wiper的宽度
          swiperStyle:{},//是wiper的样式
          sliderCount:0,//图片的个数
          currentIndex:0,//当前显示的下标
          scolling:false,//记录是否正在滚动
        }

      },
      props:{
        interval:{
          type:Number,
          default:3000
        },
        animDuration:{
          type: Number,
          default: 300
        },
        moveRate:{
          type:Number,
          default:0.25
        }
      },
      mounted() {
          console.log('页面加载完毕');
          this.handleDom();
          this.startTimer();


      },
      methods:{
        //操作dom元素
        handleDom:function () {
          let swiperEl = document.querySelector('.swiper');
          let sliderEls = document.getElementsByClassName('slide');

          //记录元素的个数
          this.sliderCount = sliderEls.length;
          if(this.sliderCount > 1){
            let cloneFirst = sliderEls[0].cloneNode(true);
            let cloneLast = sliderEls[this.sliderCount - 1].cloneNode(true);
            swiperEl.insertBefore(cloneLast , sliderEls[0]);
            swiperEl.appendChild(cloneFirst);

          }
          this.totalWidth = swiperEl.offsetWidth;
          this.swiperStyle = swiperEl.style;
          this.setTransform(-this.totalWidth);
          },
        //设置图片的显示
        setTransform(position){
          this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`;
          this.swiperStyle['-webkit-transform'] = `translate3d(${position}px), 0, 0`;
          this.swiperStyle['-ms-transform'] = `translate3d(${position}px), 0, 0`;
        },
        startTimer(){
          this.playTimer =window.setInterval(() =>{
            this.currentIndex++;
            this.setScrollCenton(-this.currentIndex * this.totalWidth)
          } , this.interval);

        },
        /**
         * 停止定时
         */
        stopTimer(){
          window.clearInterval(this.playTimer);

        },
        /**
         * 滚到正确的位置
         * @param currentPosition
         */
        setScrollCenton(currentPosition){
          this.scrolling = true;
          //开始滚动画面
          this.swiperStyle.transition = 'transform ' + this.animDuration + 'ms';

          this.setTransform(currentPosition);
          //校对位置
          this.checkPosition();
          this.scrolling = false;
        },
        /**
         * 矫正滚动的位置
         */
        checkPosition(){

          window.setTimeout(()=>{
            this.swiperStyle.transition = '0ms';
            if(this.currentIndex >= this.sliderCount + 1){
              this.currentIndex = 1;
            } else if(this.currentIndex <= 0){
              this.currentIndex = this.sliderCount;
            }
            this.setTransform(-this.currentIndex * this.totalWidth);
            // 2.结束移动后的回调
            this.$emit('transitionEnd', this.currentIndex-1);

          } , this.animDuration);

        },
        touchStart(e){
          if(this.scrolling) return;//如果正在滚动不可以拖动
          this.stopTimer();

          //保存开始时的位置
          this.startX = e.touches[0].pageX;
        },
        touchmove(e){
          //拖动的距离
          this.currentX = e.touches[0].pageX;
          this.distance = this.currentX - this.startX;
          let currentPosition = -this.currentIndex * this.totalWidth;
          let moveDistance = currentPosition + this.distance;
          this.setTransform(moveDistance);
        },
        touchend(e){
          console.log('松开时');
          //获取移动的距离
          let currentMove = Math.abs(this.distance);

          //判断最终的距离
          if(this.distance === 0)
            return;
          else if(this.distance > 0 && currentMove > this.totalWidth * this.moveRate)
            this.currentIndex--;
          else if(this.distance < 0 && currentMove > this.totalWidth * this.moveRate)
            this.currentIndex++;
          //移到正确的位置
           this.setScrollCenton(-this.currentIndex * this.totalWidth);
           this.startTimer();
        }

      }
    }
</script>

<style scoped>
  #ad-swiper{
    overflow: hidden;
    position: relative;
  }
  .swiper{
    display: flex;

  }

</style>
