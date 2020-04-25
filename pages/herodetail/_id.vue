<template>
  <div>
    <!-- 头部导航栏 -->
    <commonNav></commonNav>
    <!-- 头部广告 -->
    <topact></topact>
  </div>
</template>

<script>
import commonNav from "../../components/index/commonNav";
import topact from "../../components/index/topact";
export default {
  data() {
    return {};
  },
  components: {
    commonNav,
    topact
  },
  methods: {},
  mounted() {
      console.log(this.$route.query.heroId);
  },
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
</style>