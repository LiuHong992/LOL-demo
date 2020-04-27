<template>
  <div class="info-title f-w">{{titles}}</div>
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
.info-title {
  margin: 47px 0 15px;
  font-size: 16px;
  color: #338c7a;
}
</style>