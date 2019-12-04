<template>
  <div class="hy-swiper">
    <div class="swiper" @touchstart="touchStart" @touchmove="touchMove" @touchend="touchEnd">
      <slot></slot>
    </div>
    <slot name="indicator">
    </slot>
    <div class="indicator">
      <slot name="indicator" v-if="showIndicator && slideCount>1">
        <div class="indi-item" v-for="(item, index) in slideCount" :key="index" :class="{active:index === currentIndex-1}"></div>
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Swiper',
  data() { 
    return {
      slideCount: 0,
      totlaWidth: 0,
      currentIndex: 1,
      swiperStyle: {},
      scrolling: false
    }
  },
  props: {
    interval:{
      type: Number,
      default: 3000
    },
    animDuration: {
      type: Number,
      default: 300
    },
    moveRatio: {
      type: Number,
      default: 0.25
    },
    showIndicator: {
      type: Boolean,
      default: true
    }
  },
  components:{
  },
  mounted() {
    window.setTimeout(()=>{
      this.handleDom();

      this.startTimer();
    },100)
  },
  methods:{
    startTimer: function(){
      this.playTimer = window.setInterval(()=>{
        this.currentIndex++;
        this.scrollContent(-this.currentIndex * this.totlaWidth);
      },this.interval)
    },
    stopTimer: function(){
      window.clearInterval(this.playTimer);
    },
    scrollContent: function(currentPosition){
      this.scrolling = true;

      this.swiperStyle.transition = 'transform ' + this.animDuration + 'ms'
      this.setTransform(currentPosition);

      this.checkPosition();

      this.scrolling = false;
    },
    setTransform: function(position){
      this.swiperStyle.transform = `translate3d(${position}px, 0, 0)`
      this.swiperStyle['-webkit-transform'] = `translate3d(${position}px, 0, 0)`
      this.swiperStyle['-ms-transform'] = `translate3d(${position}px, 0, 0)`
    },
    checkPosition: function(){
      window.setTimeout(()=>{
        this.swiperStyle.transition = '0ms';

        if (this.currentIndex >= this.slideCount + 1){
          this.currentIndex = 1;
          this.setTransform(-this.currentIndex * this.totlaWidth);
        }else if (this.currentIndex <= 0){
          this.currentIndex = this.slideCount;
          this.setTransform(-this.currentIndex * this.totlaWidth);
        }

        this.$emit('transitionend', this.currentIndex - 1);
      },this.animDuration)
      
    },
    handleDom: function(){   
      let swiperEl = document.querySelector('.swiper')
      let slidesEls = document.getElementsByClassName('slide')

      this.slideCount = slidesEls.length

      if(this.slideCount > 1){
        let cloneFirst = slidesEls[0].cloneNode(true);
        let cloneLast = slidesEls[slidesEls.length-1].cloneNode(true);
        swiperEl.insertBefore(cloneLast,slidesEls[0]);
        swiperEl.appendChild(cloneFirst);
        this.totlaWidth = swiperEl.offsetWidth;
        this.swiperStyle = swiperEl.style;
      }

      this.setTransform(-this.totlaWidth);
    },
    touchStart: function(e){
      if(this.scrolling) return;

      this.stopTimer();

      this.startX = e.touches[0].pageX;
    },
    touchMove: function(e){
      this.currentX = e.touches[0].pageX;
      this.distance = this.currentX - this.startX;
      let currentPosition = -this.currentIndex * this.totlaWidth;
      let moveDistance = this.distance + currentPosition;

      this.setTransform(moveDistance);
    },
    touchEnd: function(e){
      let currentMove = Math.abs(this.distance);

      if (this.distance === 0){
        return 
      }else if (this.distance > 0 && currentMove > this.totlaWidth * this.moveRatio){
        this.currentIndex--;
      }else if (this.distance < 0 && currentMove > this.totlaWidth * this.moveRatio){
        this.currentIndex++;
      }

      this.scrollContent(-this.currentIndex * this.totlaWidth);

      this.startTimer();
    },
    previous: function(){
      this.changeItem(-1);
    },
    next: function(){
      this.changeItem(1);
    },
    changeItem: function(num){
      this.stopTimer();

      this.currentIndex += num;
      this.scrollContent(-this.currentIndex * this.totlaWidth);

      this.startTimer();
    }
  },
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
 }
</script>

<style scoped>
.hy-swiper {
  overflow: hidden;
  position: relative;
}
.swiper {
  display: flex;
}
.indicator {
  display: flex;
  justify-content: center;
  position: absolute;
  width: 100%;
  bottom: 8px;
}
.indi-item {
  box-sizing: border-box;
  width: 8px;
  height: 8px;
  line-height: 8px;
  border-radius: 4px;
  background-color: #fff;
  text-align: center;
  font-size: 12px;
  margin: 0 5px;
}
.indi-item.active {
  background-color: rgba(212, 62, 46, 1.0);
}
</style>