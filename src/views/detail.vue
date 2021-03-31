<template>
  <div class>
    <div class="top">
      <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
        <van-swipe-item v-for="(item,index) in list.images" :key="index" @click="click()">
          <img :src="item" alt />
        </van-swipe-item>
      </van-swipe>
    </div>
    <p>{{this.list.name}}</p>
    <p>{{this.list.address}}</p>
    <p>{{this.list.supportService}}</p>
  </div>
</template>
<script>
import { ImagePreview } from "vant";

export default {
  name: "",
  data() {
    return {
      list: []
    };
  },
  created() {
    this.$axios({
      url: `https://locally.uieee.com/shops/${this.$route.query.id}`
    }).then(res => {
      this.list = res.data;
      console.log(res);
    });
  },
  methods: {
    click() {
      ImagePreview(this.list.images);
    }
  }
};
</script>

<style scoped lang='scss'>
.top {
  width: 100%;
  height: 277px;

  .my-swipe .van-swipe-item {
    color: #fff;
    font-size: 20px;
    line-height: 150px;
    text-align: center;
  }
}

img {
  width: 100%;
}
</style>
