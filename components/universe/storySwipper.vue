<template>
  <div>
    <!-- 上方的图片轮播图 -->
    <div class="swiper-img-container" ref="slider" v-if="stories.length>0">
      <div class="swiper-wrapper">
        <div
          class="swiper-slide"
          v-for="(item,index) in stories"
          :key="index"
          :class="[activeIndex === index?'active-slide':'']"
        >
          <div
            class="bg-img"
            :class="[activeIndex === index?'active-slider':'']"
            :style="{'background-image':`url(${item.background.uri})`}"
          ></div>
        </div>
      </div>
    </div>
    <!-- 下方的问题内容轮播 -->
    <!-- <div class="swiper-text-container" ref="slidertwo" v-if="stories.length>0">
      <div class="swiper-wrapper">
        <div class="swiper-slide" v-for="(item,index) in stories" :key="index">
          <div class="texts" v-html="item.description"></div>
        </div>
      </div>
    </div>-->
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
      swiperText: null,
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
  methods: {},
  mounted() {
    setTimeout(() => {
      this.swiperImg = new Swiper(".swiper-img-container", {
        slidesPerView: 1,
        centeredSlides: true,
        loop: true,
        loopAdditionalSlides: 1,
        slidesOffsetBefore: 300,
        slidesOffsetAfter: 300
      });
      //   this.swiperText = new Swiper(".swiper-text-container", {
      //     slidesPerView: 1,
      //     centeredSlides: true,
      //     loop: true,
      //     controller: {
      //       control: this.swiperImg //控制swiperImg
      //     },
      //     slidesOffsetBefore: 300
      //   });
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
    }
  }
}
</style>