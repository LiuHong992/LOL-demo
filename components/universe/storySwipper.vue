<template>
  <div>
    <!-- 上方的图片轮播图 -->
    <div class="swiper-img-container p-r" ref="slider" v-if="stories.length>0">
      <div class="swiper-wrapper">
        <div
          class="swiper-slide swiper-no-swiping"
          v-for="(item,index) in stories"
          :key="index"
          :class="[activeIndex === index?'active-slide':'']"
        >
          <div
            class="bg-img"
            :class="[activeIndex === index?'active-slider':'']"
            :style="{'background-image':`url(${item.background.uri})`}"
          ></div>
          <div class="texts" v-html="item.description" @click="handleClick(index)"></div>
        </div>
      </div>
      <div class="swiper-button-prev" style="left:186px"></div>
      <div class="swiper-button-next" style="right:170px"></div>
    </div>
  </div>
</template>

<script>
import Swiper from "swiper";
export default {
  data() {
    return {
      // 轮播图实例
      swiperImg: null,
      // 第二个轮播图实例
      // swiperText: null,
      // 当前选中的轮播图
      activeIndex: 0
    };
  },
  props: {
    stories: {
      type: Array,
      default: () => []
    }
  },
  components: {},
  methods: {
    // 文字点击事件
    handleClick(idx) {
      console.log(idx);
      if (idx === this.activeIndex - 1) {
        this.swiperImg.slidePrev();
      } else if (idx === this.activeIndex + 1) {
        this.swiperImg.slideNext();
      }
      console.log(idx);
    }
  },
  mounted() {
    setTimeout(() => {
      this.swiperImg = new Swiper(".swiper-img-container", {
        slidesPerView: 1,
        centeredSlides: true,
        loop: true,
        noSwiping: true, //图片轮播图不能通过滑动图片切换
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev"
        },
        loopAdditionalSlides: 1,
        slidesOffsetBefore: 300,
        slidesOffsetAfter: 300
      });
      // this.swiperText = new Swiper(".swiper-text-container", {
      //   slidesPerView: 1,
      //   centeredSlides: true,
      //   loop: true,
      //   navigation: {
      //     nextEl: ".swiper-button-next",
      //     prevEl: ".swiper-button-prev"
      //   },
      //   controller: {
      //     control: this.swiperImg //控制swiperImg
      //   },
      //   loopAdditionalSlides: 1,
      //   slidesOffsetBefore: 300
      // });
    }, 100);
  },
  watch: {
    "swiperImg.realIndex"(val) {
      this.activeIndex = val;
      //   if (oldVal === 4) {
      //     this.$nextTick(() => {
      //       this.swiperImg.init(); // 再初始化swiper
      //     });
      //   }
      console.log(val);
    }
  },
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
@import "../../node_modules/swiper/css/swiper";
.swiper-img-container {
  height: 315px;
  margin-top: 30px;
  --swiper-navigation-color: #9c7e43; /* 单独设置按钮颜色 */
  --swiper-navigation-size: 30px; /* 设置按钮大小 */
  .swiper-wrapper {
    .swiper-slide {
      .bg-img {
        width: 100%;
        transform: scale(1);
        filter: grayscale(100%) brightness(0.3);
        transition: all 0.8s ease;
        height: 100%;
        background-position: 50% 50%;
        opacity: 1;
        background-size: cover;
      }
      .texts {
        color: #c4b998;
        font-size: 12px;
        line-height: 1.4;
        padding: 0 50px 20px;
        position: relative;
      }
      .active-slider {
        filter: grayscale(0) brightness(1);
        transform: scale(1.2);
        animation-duration: 0.6s;
        box-shadow: 0 0 16px 14px rgba(0, 0, 0, 0.4);
      }
    }
    .active-slide {
      width: 61% !important;
      z-index: 10;
    }
  }
}
.swiper-text-container {
  .swiper-wrapper {
    .swiper-slide {
      width: 506px !important;
      height: 180px;
    }
  }
}
</style>