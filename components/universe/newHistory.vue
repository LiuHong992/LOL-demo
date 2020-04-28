<template>
  <div class="history-wraper">
    <ul>
      <li
        class="items p-r"
        :class="[index===2?'special-item':'']"
        v-for="(item,index) in storyArr"
        :key="index"
        :style="{float:index===2?'right':'left'}"
      >
        <commonBox :commonItem="item" :storyType="storyType"></commonBox>
      </li>
      <li class="clear-item"></li>
    </ul>
  </div>
</template>

<script>
import commonBox from "./commonBox";
export default {
  data() {
    return {};
  },
  props: {
    storyArr: {
      type: Array,
      default: () => []
    },
    storyType: {
      type: String,
      default: ""
    }
  },
  components: {
    commonBox
  },
  methods: {},
  mounted() {},
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
.history-wraper {
  margin: 200px auto 60px;
  max-width: 1280px;
  ul {
    list-style: none;
    margin: -0.5em;
    padding-left: 0;
    li {
      vertical-align: top;
    }
    .items {
      width: calc(25% - 1em);
      transition-property: transform, z-index, border;
      transition-duration: 0.3s, 0.3s, 0.3s;
      background-color: #101217;
      border: 1px solid #32281f;
      box-shadow: 0 0 16px 14px rgba(0, 0, 0, 0.4);
      color: #c4b998;
      cursor: pointer;
      //   display: inline;
      height: 340px;
      margin: 0.5em;
      overflow: hidden;
      z-index: 1;
      &:hover {
        z-index: 15 !important;
        transition-timing-function: ease, step-start;
        border: 1px solid #927345;
        transform: scale(1.1);
      }
    }
    .special-item {
      width: calc(50% - 1em);
      height: calc(680px + 1em);
    }
    // 清除浮动
    .clear-item::after {
      content: "";
      display: table;
      clear: both;
    }
  }
}
</style>