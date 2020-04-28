<template>
  <div class="common-item fl f-end p-r w-100">
    <!-- 背景图片 -->
    <div
      class="bg-image p-a"
      :class="[storyType==='精选'?'spePos':'']"
      :style="{'background-image':`url(${commonItem.background.uri})`}"
    ></div>
    <!-- 下方内容层 -->
    <div class="bottom-cont">
      <!-- 显示在视图层的内容 -->
      <div class="show-cont p-r t-center">
        <!-- 上方的图标 -->
        <div class="icon-img p-a fl a-c f-center">
          <img
            src="//game.gtimg.cn/images/lol/universe/images/content_type_icon_faction__14mjH.png"
            alt
            v-if="commonItem.type === 'link-out' && storyType==='最新'"
          />
          <img
            src="data:image/png;base64,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"
            alt
            v-if="commonItem.type==='story-preview' && storyType==='最新'"
          />
          <img
            src="//game.gtimg.cn/images/lol/universe/images/content_type_icon_champion__3nwJQ.png"
            alt
            v-if="storyType==='精选'"
          />
        </div>
        <!-- 下方的标题 -->
        <h3 v-if="commonItem.type==='story-preview' && storyType==='最新'">
          <span class="f-w title-sp f-s-12 t-center">
            <span>短篇故事</span>
          </span>
        </h3>
        <!-- 下方的标题 -->
        <h3 v-if=" storyType==='精选'">
          <span class="f-w title-sp f-s-12 t-center">
            <span>{{commonItem.subtitle}}</span>
          </span>
        </h3>
        <h1 class="f-s-14 t-center">{{commonItem.title}}</h1>
      </div>
      <!-- 隐藏在下方的内容 -->
      <div class="hidden-cont t-center f-s-12">
        <span>了解更多</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    commonItem: {
      type: Object,
      default: () => {}
    },
    storyType: {
      type: String,
      default: ""
    }
  },
  components: {},
  methods: {},
  mounted() {},
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
.common-item {
  flex-direction: column;
  background-color: #101217;
  height: 100%;
  &:hover {
    .hidden-cont {
      height: 54px !important;
    }
  }
  .bg-image {
    top: 0;
    right: 0;
    bottom: 40px;
    left: 0;
    background-size: cover;
    background-position: 50% 50%;
  }
  .spePos {
    background-position: 76% 3%;
  }
  .bottom-cont {
    background-color: #101217;
    z-index: 5;
    .show-cont {
      height: 80px;
      padding: 29px 12px;
      background-color: #101217;
      border-top: 1px solid #7e633b;
      z-index: 10;
      .icon-img {
        top: -21px;
        right: calc(50% - 21px);
        height: 42px;
        width: 42px;
        background-color: #101217;
        border-radius: 50%;
        img {
          max-height: 21px;
          max-width: 21px;
        }
      }
      .icon-img::after {
        position: absolute;
        top: -2px;
        right: -2px;
        bottom: -2px;
        left: -2px;
        background-image: linear-gradient(
          180deg,
          #3e3310,
          #806734,
          #c6b98b,
          #806734,
          #3e3310
        );
        border-radius: 50%;
        box-shadow: 0 0 20px 12px rgba(0, 0, 0, 0.2);
        content: "";
        z-index: -1;
      }
      h3 {
        padding-bottom: 3px;
        .title-sp {
          display: block;
          color: #937341 !important;
          letter-spacing: 2px;
          text-transform: uppercase;
          padding-bottom: 0;
        }
      }
      h1 {
        font-weight: 400;
        color: #c4b998;
        letter-spacing: 2px;
        text-transform: uppercase;
      }
    }
    .hidden-cont {
      border-top: 1px solid #7e633b;
      height: 0;
      font-weight: 400;
      transition: 0.4s ease;
      background-color: #14181d;
      color: #937341;
      letter-spacing: 0.3em;
      line-height: 54px;
      overflow: hidden;
      text-transform: uppercase;
      z-index: 3;
    }
  }
}
</style>