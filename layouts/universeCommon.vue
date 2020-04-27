<template>
  <div>
    <el-container>
      <el-header>
        <div class="header-container fl s-b a-c">
          <!-- 左边的图片 -->
          <div class="left-img">
            <img class="img" src="https://game.gtimg.cn/images/lol/universe/images/1.jpg" alt />
          </div>
          <!-- 中间的内容层 -->
          <div class="center-content fl">
            <div
              class="nav-each"
              :class="[item.isActive?'':'empty',activeNav===index?'is-active':'']"
              v-for="(item,index) in universeNav"
              :key="index"
              @click="goTo(item,index)"
            >
              <div>{{item.cnTitle}}</div>
              <div>{{item.enTitle}}</div>
            </div>
          </div>
          <!-- 最右边的链接 -->
          <div>
            <a
              class="headr-right"
              href="http://weibo.com/u/6090640055?refer_flag=1001030101_"
              title="故事微博"
              target="_blank"
            ></a>
          </div>
        </div>
      </el-header>
      <el-main>
        <nuxt></nuxt>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 顶部导航栏
      universeNav: [
        {
          cnTitle: "专题",
          enTitle: "FEATURED",
          paths: "/universe",
          isActive: true
        },
        {
          cnTitle: "英雄",
          enTitle: "CHAMPIONS",
          paths: "/champions",
          isActive: true
        },
        {
          cnTitle: "开发中",
          enTitle: "DEVELOP"
        },
        {
          cnTitle: "开发中",
          enTitle: "DEVELOP"
        },
        {
          cnTitle: "开发中",
          enTitle: "DEVELOP"
        },
        {
          cnTitle: "开发中",
          enTitle: "DEVELOP"
        }
      ],
      // 当前选中的导航栏
      activeNav: 0
    };
  },
  components: {},
  methods: {
    // 跳转
    goTo(item, idx) {
      if (item.paths) {
        this.activeNav = idx;
        this.$router.push(item.paths);
      }
    }
  },
  mounted() {
    if (this.$route.path) {
      this.universeNav.map((item, index) => {
        if (item.paths === this.$route.path) {
          this.activeNav = index;
        }
      });
    }
  },
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
.el-header {
  border-bottom: 2px solid #262626;
  background: #121212;
  .header-container {
    height: 100%;
    .center-content {
      .nav-each {
        color: #c9aa71;
        font-size: 14px;
        padding: 8px 0;
        border-bottom: 1px solid transparent;
        margin: 0 20px;
        cursor: pointer;
        text-align: center;
      }
      .empty {
        color: gray;
        cursor: not-allowed;
      }
      .is-active {
        color: #fff;
        border-bottom: 1px solid #c79a3c;
      }
    }
    .headr-right {
      background: url(//game.gtimg.cn/images/lol/universe/images/4.jpg)
        no-repeat 0 0;
      text-indent: -9999px;
      overflow: hidden;
      text-align: left;
      height: 32px;
      width: 121px;
      color: #bb9e69;
      font-size: 11px;
      font-weight: 700;
      display: inline-block;
    }
  }
}
</style>