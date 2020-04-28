<template>
  <div class="comon-title p-r t-center">
    <!-- 图片 -->
    <img
      class="title-img p-a"
      src="//game.gtimg.cn/images/lol/universe/images/content_type_icon_latest__1ulWu.png"
      alt
    />
    <!-- 中间的具体标题内容 -->
    <h1>
      <span>
        <!-- 左边 -->
        <span>
          <span>
            <img
              class="left-img imgs"
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAARcAAAABCAYAAAD0K+rmAAAA80lEQVR4AV2TiW0EMQwDh72loqSTFGwF8A0Exnu/xW/pc35/vr5DmBlIBvyRwP3I3BnctfC5XAMy5LOQC8ZBcZO7UNwBQUQr/cUHNNVMDYaLxhHwZpvmiJqE9l3pJOKfmYQX2zmTUPerj5jtBRKVBBl0dNjf97Hft99jl29vynHucPUGzN55txnS3U3XHHH/feh96WzH5CcJi1c0Jf70OJj3s65mwfXzc/s527ncxnbWaNkz+6p9XE5zJYoB7HQ3IHbQRa/2q9P59Nl7qrfmbzf9HwI0Kq6Dx9f55hS0fejkedg+BSjs+XvP5NM/67k4ATr/AU/oIFuGMAGgAAAAAElFTkSuQmCC"
              alt
            />
          </span>
          <span class="icons left-icon p-r"></span>
        </span>
        <!-- 中间span -->
        <span class="center-sp p-r">
          <span>{{titles}}</span>
        </span>
        <!-- 右边span -->
        <span>
          <span class="icons p-r right-icon"></span>
          <span>
            <img
              class="right-img imgs"
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAARcAAAABCAYAAAD0K+rmAAAA80lEQVR4AV2TiW0EMQwDh72loqSTFGwF8A0Exnu/xW/pc35/vr5DmBlIBvyRwP3I3BnctfC5XAMy5LOQC8ZBcZO7UNwBQUQr/cUHNNVMDYaLxhHwZpvmiJqE9l3pJOKfmYQX2zmTUPerj5jtBRKVBBl0dNjf97Hft99jl29vynHucPUGzN55txnS3U3XHHH/feh96WzH5CcJi1c0Jf70OJj3s65mwfXzc/s527ncxnbWaNkz+6p9XE5zJYoB7HQ3IHbQRa/2q9P59Nl7qrfmbzf9HwI0Kq6Dx9f55hS0fejkedg+BSjs+XvP5NM/67k4ATr/AU/oIFuGMAGgAAAAAElFTkSuQmCC"
              alt
            />
          </span>
        </span>
      </span>
    </h1>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    titles: {
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
.comon-title {
  font-weight: 400;
  top: 145px;
  .title-img {
    opacity: 1;
    top: -40px;
    left: calc(50% - 16px);
    transition: opacity 0.6s ease;
    max-width: 32px;
    max-height: 32px;
  }
  h1 {
    color: #c4b998;
    .center-sp {
      opacity: 1;
      transition: 0.6s;
      transition-delay: 0.1s;
      color: #c4b998;
      font-size: 24px;
      letter-spacing: 7px;
      text-indent: 8px;
      text-transform: uppercase;
      top: 4px;
    }
    .icons {
      background: #373121;
      font-size: 0;
      z-index: 100;
    }
    .icons::before {
      height: 5px;
      width: 5px;
      position: absolute;
      top: -9px;
      left: -77px;
      //   -webkit-transform: rotate(45deg);
      //   -moz-transform: rotate(45deg);
      //   -ms-transform: rotate(45deg);
      //   -o-transform: rotate(45deg);
      transform: rotate(45deg);
      border: 1px solid #373121;
      content: "\25C7";
      font-size: 0;
    }
    .right-icon::before {
      position: absolute;
      left: 65px;
    }
    .left-img {
      transform: rotate(180deg);
    }
    .imgs {
      padding-left: 70px;
      vertical-align: middle;
      width: 30%;
    }
  }
}
</style>