<template>
  <div class>
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
      <van-swipe-item v-for="item in imgList" :key="item.id">
        <img :src="item.image" alt />
      </van-swipe-item>
    </van-swipe>
    <van-grid :border="false" :column-num="3">
      <van-grid-item v-for="ele in gitList" :key="ele.id" @click="toGit(ele.id)">
        <img :src="ele.icon" alt />
        <p>{{ele.name}}</p>
      </van-grid-item>
    </van-grid>
  </div>
</template>

<script>
export default {
  name: "",
  data() {
    return {
      imgList: [],
      gitList: []
    };
  },
  created() {
    this.$axios({
      url: "https://locally.uieee.com/slides"
    }).then(res => {
      this.imgList = res.data;
    });

    this.$axios({
      url: "https://locally.uieee.com/categories"
    }).then(res => {
      this.gitList = res.data;
    });
  },
  methods: {
    toGit(id) {
      this.$router.push({ path: "/list", query: { id } });
    }
  }
};
</script>

<style scoped lang='scss'>
.my-swipe .van-swipe-item {
  color: #fff;
  font-size: 20px;
  line-height: 150px;
  text-align: center;
}
img {
  width: 100%;
  height: 100%;
}
</style>