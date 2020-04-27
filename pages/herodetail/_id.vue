<template>
  <div>
    <!-- 头部导航栏 -->
    <commonNav></commonNav>
    <!-- 头部广告 -->
    <topact></topact>
    <!-- 下方内容层 -->
    <div class="wraper m-auto">
      <!-- 内容显示区域 -->
      <div class="layout p-r">
        <!-- 皮肤轮播和英雄信息 -->
        <swipper :heroObj="heroObj" :skinArr="skinArr"></swipper>
        <!-- 下方更多内容 -->
        <div class="clearfix">
          <!-- 左边内容层 -->
          <div class="infoleftcont">
            <!-- 背景故事标题 -->
            <common-title titles="背景故事"></common-title>
            <!-- 背景故事盒子 -->
            <div class="colbox bgstory f-s-14 l-h-24">
              <!-- 故事内容 -->
              <div class="lore" :class="moreFlag?'t-over-4':''">{{heroObj.shortBio}}</div>
              <!-- 查看更多 -->
              <span class="cgray" v-if="moreFlag" @click="moreFlag = false">查看更多...</span>
              <!-- 收起 -->
              <span class="cgray" v-else @click="moreFlag = true">收起...</span>
            </div>
            <!-- 技能介绍标题 -->
            <common-title titles="技能介绍"></common-title>
            <!-- 技能介绍 -->
            <spellsIntro :spellArr="spellArr"></spellsIntro>
            <!-- 使用技巧标题 -->
            <common-title titles="使用技巧"></common-title>
            <!-- 使用技巧 -->
            <div class="colbox arttips">
              <!-- 当自己使用时 -->
              <dl class="borlineX">
                <dt class="f-s-14 f-w">当你使用{{heroObj.name}}</dt>
                <dd>
                  <p v-for="(item,index) in heroObj.allytips" :key="index">{{item}}</p>
                </dd>
              </dl>
              <!-- 当敌方使用时 -->
              <dl>
                <dt class="f-s-14 f-w">敌人使用{{heroObj.name}}</dt>
                <dd>
                  <p v-for="(item,index) in heroObj.enemytips" :key="index">{{item}}</p>
                </dd>
              </dl>
            </div>
          </div>
          <!-- 右边我的记录 -->
          <div class="inforightcont">
            <!-- 我的记录标题 -->
            <common-title titles="我的记录"></common-title>
            <div class="colbox">
              <div class="cont f-s-12">
                您无法查看使用该英雄的记录，请
                <span>[登陆]</span>，并绑定所在大区。
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import commonNav from "../../components/index/commonNav";
import topact from "../../components/index/topact";
import swipper from "../../components/herodetail/swipper";
import spellsIntro from "../../components/herodetail/spellsIntro";
export default {
  data() {
    return {
      // 接收传递过来的英雄id值
      hId: "",
      // 接收请求到的英雄基本信息
      heroObj: {},
      // 接收请求到的英雄的皮肤
      skinArr: [],
      // 接收请求到的英雄的技能信息
      spellArr: [],
      // 查看更多按钮
      moreFlag: true
    };
  },
  components: {
    commonNav,
    topact,
    swipper,
    spellsIntro
  },
  methods: {
    // 请求英雄信息的方法
    getHeroDetail(id) {
      this.$api
        .getHeroById(id)
        .then(res => {
          if (res) {
            this.heroObj = res.hero;
            // 皮肤数据处理
            this.skinArr = res.skins.filter(item => {
              return item.chromasBelongId === "0";
            });
            let numArr = [1, 2, 4, 0, 3];
            numArr.map(item => {
              this.spellArr.push(res.spells[item]);
            });
            console.log(this.heroObj);
            console.log(this.skinArr);
            console.log(this.spellArr);
          }
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  mounted() {
    this.hId = this.$route.query.heroId;
    if (this.hId !== "") {
      this.getHeroDetail(this.hId);
    }
  },
  watch: {},
  computed: {},
  filters: {}
};
</script>

<style scoped lang='scss'>
.wraper {
  min-width: 1240px;
  background: #f7f8f8;
  color: #666;
  overflow: hidden;
  .layout {
    width: 1240px;
    overflow: hidden;
    margin: 50px auto;
    .clearfix {
      .infoleftcont {
        float: left;
        width: 63%;
        .bgstory {
          padding: 28px 32px;
          text-indent: 2em;
          .cgray {
            cursor: pointer;
            color: #999;
            line-height: 40px;
          }
        }
        .arttips {
          padding: 20px 30px 10px;
          dl {
            padding-bottom: 15px;
            margin-bottom: 20px;
            font-size: 14px;
            color: #333;
            dt {
              color: #338c7a;
              padding-bottom: 8px;
            }
            dd {
              p {
                padding-bottom: 10px;
              }
            }
          }
          .borlineX {
            border-bottom: 1px solid #eee;
          }
        }
      }
      .inforightcont {
        float: right;
        width: 35%;
        .cont {
          padding: 35px 0 22px 20px;
          width: 311px;
          span {
            cursor: pointer;
            color: #00a483;
          }
        }
      }
    }
  }
}
</style>