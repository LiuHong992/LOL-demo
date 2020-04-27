<template>
  <div>
    <!-- 头部的故事轮播图 -->
    <storySwipper :stories="headSwipper"></storySwipper>
  </div>
</template>

<script>
import storySwipper from "../../components/universe/storySwipper";
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
    storySwipper
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
</style>