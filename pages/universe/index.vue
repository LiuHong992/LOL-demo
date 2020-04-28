<template>
  <div>
    <!-- 头部的故事轮播图 -->
    <storySwipper :stories="headSwipper"></storySwipper>
    <!-- 最新数据模块 -->
    <div class="latest-wraper p-r">
      <!-- 背景层 -->
      <div
        class="latest-bg p-a"
        style="background:url('//game.gtimg.cn/images/lol/universe/images/latestBg.jpg')"
      >
        <div class="bg-content p-a"></div>
      </div>
      <!-- 标题 -->
      <uniTitle titles="最新"></uniTitle>
      <newHistory :storyArr="latestArr" storyType="最新"></newHistory>
    </div>
    <!-- 精选数据模块 -->
    <div class="special-wraper p-r">
      <!-- 背景层 -->
      <div
        class="latest-bg p-a"
        style="background:url('//game.gtimg.cn/images/lol/universe/images/trendingBackground.jpg')"
      >
        <div class="bg-content p-a"></div>
      </div>
      <!-- 标题 -->
      <uniTitle titles="精选"></uniTitle>
      <newHistory :storyArr="specialArr" storyType="精选"></newHistory>
    </div>
  </div>
</template>

<script>
import storySwipper from "../../components/universe/storySwipper";
import uniTitle from "../../components/universe/uniTitle";
import newHistory from "../../components/universe/newHistory";
export default {
  data() {
    return {
      // 接收头部轮播图数据
      headSwipper: [],
      // 接收最新数据
      latestArr: [],
      // 接收精选数据
      specialArr: [],
      // 接收底部亮点英雄的数据
      lightArr: [],
      // 接收亮点地区的数据
      lightAreaArr: []
    };
  },
  layout: "universeCommon",
  components: {
    storySwipper,
    uniTitle,
    newHistory
  },
  methods: {
    // 获取专题内容的方法
    getUniverse() {
      this.$api
        .getExplore()
        .then(res => {
          if (res) {
            this.headSwipper = res["hero-modules"];
            this.latestArr = res["latest-modules"];
            this.specialArr = res["trending-modules"];
            this.lightArr = res["featured-champions"];
            this.lightAreaArr = res["featured-factions"];
            console.log(this.headSwipper);
            console.log(this.latestArr);
            console.log(this.specialArr);
            console.log(this.lightArr);
            console.log(this.lightAreaArr);
          }
          //   console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  mounted() {
    this.getUniverse();
  },
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
.latest-wraper,
.special-wraper {
  opacity: 1;
  clear: both;
  height: auto;
  transition: opacity 1.4s ease;
  .latest-bg {
    background-position: 50% !important;
    background-size: cover !important;
    top: -250px;
    right: 0;
    bottom: 51%;
    left: 0;
    opacity: 0.15;
    .bg-content {
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      background-color: #0a0a0c;
      background-image: linear-gradient(
        180deg,
        #0a0a0c,
        rgba(0, 0, 0, 0),
        #0a0a0c
      );
      background-color: rgba(0, 0, 0, 0);
    }
  }
}
</style>