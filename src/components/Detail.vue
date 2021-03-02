<template>
  <div class="big">
    <div class="box">
      <img :src="img" alt class="img" @click="i" />
      <p class="p1">{{name}}</p>
      <p class="p2" @click="$router.go(-1)">
        <van-icon name="arrow-left" class="i" />
      </p>
    </div>
    <van-cell-group v-for="(item,key) in list" :key="key">
      <van-cell :title="item.title" icon="fire" />
      <van-cell-group v-for="(item1,key) in item.children" :key="key" class="t">
        <van-cell :title="item1.title" icon="fire" />
        <van-cell-group v-for="(item2,key) in item1.children" :key="key" class="tt">
          <van-cell :title="item2.title" icon="fire" />
        </van-cell-group>
      </van-cell-group>
    </van-cell-group>
  </div>
</template>

<script>
import { ImagePreview } from "vant";
export default {
  data() {
    return {
      img: "",
      name: "",
      img2: [],
      list: []
    };
  },
  mounted() {
    this.$http.get("/mock/detail.json").then(res => {
      console.log(res);
      this.img = res.data.data.bannerImg;
      this.name = res.data.data.sightName;
      this.img2 = res.data.data.gallaryImgs;
      this.list = res.data.data.categoryList;
    });
  },
  methods: {
    i() {
      ImagePreview(this.img2);
    }
  }
};
</script>

<style lang="scss" scoped>
.big{
  width: 100%;
  height: 100%;
}
.img {
  width: 100%;
  height: 206px;
}
.box {
  position: relative;
  width: 100%;
  height: 206px;
}
.p1 {
  position: absolute;
  bottom: 5px;
  left: 5px;
  color: #fff;
}
.p2 {
  width: 40px;
  height: 40px;
  position: absolute;
  top: 5px;
  left: 5px;
  background: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.i {
  font-size: 26px;
  color: #fff !important;
}
.van-icon {
  color: rgb(60, 212, 250);
}
.t{
  padding-left: 8px;
}
.tt{
  padding-left: 16px;
}
</style>