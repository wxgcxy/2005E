<template>
  <div class>
    <van-card
      v-for="item in list"
      :key="item.id"
      :desc="item.businessHours"
      :title="item.address"
      :thumb="item.images[0]"
      @click="toDetail(item.id)"
      lazy-load
    />
  </div>
</template>

<script>
import Vue from "vue";
import { Lazyload } from "vant";
Vue.use(Lazyload);
// 注册时可以配置额外的选项
Vue.use(Lazyload, {
  lazyComponent: true
});
export default {
  name: "",
  data() {
    return {
      list: []
    };
  },
  created() {
    this.$axios({
      url: `  https://locally.uieee.com/categories/${this.$route.query.id}/shops`
    }).then(res => {
      this.list = res.data;
    });
  },
  methods: {
    toDetail(id) {
      this.$router.push({
        path: "/detail",
        query: { id }
      });
    }
  }
};
</script>

<style scoped lang='scss'>

</style>