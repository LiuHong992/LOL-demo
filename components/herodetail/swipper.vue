<template>
  <div class="swipper-wraper p-r">
    <!-- 左边的背景 -->
    <div class="sbg p-a"></div>
    <!-- 悬浮于背景上的英雄信息 -->
    <div class="detail-data p-a" v-if="heroObj.heroId">
      <!-- 英雄称号 -->
      <div class="name">{{heroObj.name}}</div>
      <!-- 英雄姓名 -->
      <div class="title">{{heroObj.title}}</div>
      <!-- 标签 -->
      <div class="tags">
        <el-tag
          class="m-r-5"
          size="mini"
          type="success"
          effect="dark"
          v-for="(item,index) in heroObj.roles"
          :key="index"
        >{{item | tagsRole}}</el-tag>
      </div>
      <!-- 英雄能力表 -->
      <div class="info">
        <!-- 物理攻击 -->
        <dt>物理攻击</dt>
        <dd>
          <i class="up up1" :style="{width:heroObj.attack*10+'%'}"></i>
        </dd>
        <!-- 魔法攻击 -->
        <dt>魔法攻击</dt>
        <dd>
          <i class="up up2" :style="{width:heroObj.magic*10+'%'}"></i>
        </dd>
        <!-- 防御能力 -->
        <dt>防御能力</dt>
        <dd>
          <i class="up up3" :style="{width:heroObj.defense*10+'%'}"></i>
        </dd>
        <!-- 上手难度 -->
        <dt>上手难度</dt>
        <dd>
          <i class="up up4" :style="{width:heroObj.difficulty*10+'%'}"></i>
        </dd>
      </div>
      <!-- 购买按钮 -->
      <div class="buy-btn">
        <div class="btn">购买英雄</div>
      </div>
    </div>
    <!-- 皮肤轮播 -->
    <div class="hero-skins p-r w-100" v-if="skinArr.length>0">
      <!-- 皮肤ul -->
      <ul class="p-r skin-bg" :style="{left:offsetLeft+'px'}">
        <li v-for="(item,index) in skinArr" :key="index" :title="item.name">
          <img :src="item.mainImg" />
        </li>
      </ul>
      <!-- 皮肤小图 -->
      <div class="hero-skin-nav p-a">
        <!-- 皮肤名字 -->
        <div class="hero-skin-name">
          <span>{{currentName}}</span>
        </div>
        <!-- 皮肤小图ul -->
        <ul>
          <li
            class="p-r"
            v-for="(item,index) in skinArr"
            :key="index"
            @click="changeCurrent(index)"
          >
            <!-- 图片 -->
            <img width="60" height="60" :src="item.iconImg" />
            <!-- 外边框(当前选中项) -->
            <span class="sbor p-a" v-if="currentNum === index"></span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
let t;
export default {
  data() {
    return {
      // 英雄分类参数
      heroGroup: [
        {
          faTitle: "战士",
          faRole: "fighter"
        },
        {
          faTitle: "法师",
          faRole: "mage"
        },
        {
          faTitle: "刺客",
          faRole: "assassin"
        },
        {
          faTitle: "坦克",
          faRole: "tank"
        },
        {
          faTitle: "射手",
          faRole: "marksman"
        },
        {
          faTitle: "辅助",
          faRole: "support"
        }
      ],
      // 当前皮肤名字
      currentName: "",
      // 当前选中皮肤的下标
      currentNum: 0
    };
  },
  props: {
    heroObj: {
      type: Object,
      default: () => {}
    },
    skinArr: {
      type: Array,
      default: () => []
    }
  },
  components: {},
  methods: {
    // 切换当前皮肤图片
    changeCurrent(idx) {
      this.currentNum = idx;
      this.currentName = this.skinArr[this.currentNum].name;
    }
  },
  beforeCreate() {
    t = this;
  },
  mounted() {
    setTimeout(() => {
      this.currentName = this.skinArr[this.currentNum].name;
    }, 500);
    // console.log(this.skinArr[this.currentNum].name);
  },
  watch: {},
  computed: {
    offsetLeft() {
      return 0 - this.currentNum * 1240;
    }
  },
  filters: {
    // 职业定位
    tagsRole(data) {
      let role = "";
      t.heroGroup.map(item => {
        if (item.faRole === data) {
          role = item.faTitle;
        }
      });
      return role;
    }
  }
};
</script>

<style scoped lang='scss'>
.swipper-wraper {
  height: 632px;
  .sbg {
    top: 0;
    left: 0;
    width: 305px;
    height: 100%;
    z-index: 2;
    background: #000;
    opacity: 0.6;
  }
  .detail-data {
    top: 50px;
    left: 40px;
    width: 290px;
    color: #fff;
    z-index: 3;
    .name {
      font-size: 24px;
      line-height: 25px;
      padding-bottom: 5px;
      font-weight: 400;
    }
    .title {
      height: 60px;
      font-size: 42px;
      padding-bottom: 30px;
      font-weight: 700;
    }
    .tags {
      overflow: hidden;
    }
    .info {
      margin-top: 25px;
      height: 90px;
      width: 150px;
      dt {
        font-size: 12px;
        float: left;
        width: 40%;
        margin-bottom: 5px;
        height: 16px;
        line-height: 16px;
      }
      dd {
        float: left;
        width: 60%;
        margin: 2px 0 7px;
        height: 12px;
        background: #363c3c;
        .up {
          display: block;
          height: 12px;
        }
        .up1 {
          background: #f2c500;
        }
        .up2 {
          background: #f59d00;
        }
        .up3 {
          background: #2c97de;
        }
        .up4 {
          background: #1eca6b;
        }
      }
    }
    .buy-btn {
      margin-top: 25px;
      cursor: pointer;
      .btn {
        display: block;
        width: 153px;
        height: 40px;
        overflow: hidden;
        text-indent: -999em;
        background-position: -638px 0;
        background-repeat: no-repeat;
        background-image: url(//game.gtimg.cn/images/lol/web201310/page.png?d=20131230);
      }
    }
  }
  .hero-skins {
    height: 632px;
    overflow: hidden;
    .skin-bg {
      transition: left 0.5s;
      width: 20000px;
      padding: 0;
      li {
        list-style: none;
        float: left;
        width: 1240px;
        img {
          width: 1240px;
          height: 632px;
        }
      }
    }
    .hero-skin-nav {
      bottom: 10px;
      right: 10px;
      padding-left: 306px;
      .hero-skin-name {
        padding-bottom: 10px;
        text-align: right;
        span {
          padding: 0 5px;
          background-color: #000;
          font-size: 20px;
          line-height: 25px;
          color: #fff;
        }
      }
      ul {
        li {
          cursor: pointer;
          list-style: none;
          float: left;
          .sbor {
            top: 0;
            left: 0;
            display: block;
            width: 60px;
            height: 60px;
            border: 4px solid #00a483;
          }
        }
      }
    }
  }
}
</style>