<template>
  <div class="spell-wraper">
    <!-- 所有的技能图标 -->
    <ul class="infotab p-r">
      <li
        @click="changeNow(index)"
        v-for="(item,index) in spellArr"
        :key="index"
        :class="nowSpell===index?'current':''"
      >
        <img :src="item.abilityIconPath" />
      </li>
    </ul>
    <!-- 当前技能描述 -->
    <div class="colbox infoskillbox p-r" v-if="spellArr.length>0">
      <!-- 技能标题 -->
      <div class="skilltitle">
        <!-- 技能名称 -->
        <span class="sp-name m-r-10 f-w">{{spellArr[nowSpell].name}}</span>
        <!-- 快捷键 -->
        <em v-if="spellArr[nowSpell].spellKey === 'passive'">被动技能</em>
        <em v-else>快捷键：{{spellArr[nowSpell].spellKey | upLetters}}</em>
      </div>
      <!-- 技能描述 -->
      <p class="skilltip">{{spellArr[nowSpell].description}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 当前选中项
      nowSpell: 0
    };
  },
  props: {
    spellArr: {
      type: Array,
      default: () => []
    }
  },
  components: {},
  methods: {
    // 改变当前技能
    changeNow(idx) {
      this.nowSpell = idx;
    }
  },
  mounted() {},
  watch: {},
  computed: {},
  filters: {
    upLetters(data) {
      return data.toUpperCase();
    }
  }
};
</script>

<style scoped lang='scss'>
.spell-wraper {
  .infotab {
    height: 90px;
    z-index: 2;
    overflow: hidden;
    padding: 0;
    li {
      list-style: none;
      float: left;
      width: 64px;
      height: 64px;
      padding: 13px 20px;
      cursor: pointer;
      box-sizing: content-box;
    }
    .current {
      border-top: 3px solid #00a383;
      padding: 10px 19px 13px;
      background: #fff;
      border-left: 1px solid #e1e1e1;
      border-right: 1px solid #e1e1e1;
    }
  }
  .infoskillbox {
    padding: 20px 30px;
    margin-top: -1px;
    z-index: 1;
    .skilltitle {
      padding-bottom: 10px;
      font-size: 14px;
      color: #999;
      .sp-name {
        color: #333;
      }
      em {
        font-style: normal;
      }
    }
    .skilltip {
      color: #333;
      padding-bottom: 10px;
      line-height: 19.5px;
      font-size: 12px;
    }
  }
}
</style>