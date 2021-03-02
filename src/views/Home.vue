<template>
  <div class="home">
    <header>
      <van-icon name="arrow-left" class="i" />
      <van-search v-model="value" shape="round" background="#00c5c3" placeholder="请输入搜索关键词" />
      <p class="p1" @click="$router.push('/city')">北京</p>
    </header>
    <div class="content">
      <div class="box">
        <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
          <van-swipe-item v-for="(item,key) in list" :key="key">
            <img :src="item.imgUrl" alt />
          </van-swipe-item>
        </van-swipe>
      </div>
      <van-swipe class="my-swipe1" indicator-color="white">
        <van-swipe-item>
          <ul class="u1">
            <li v-for="(item,key) in icon1" :key="key">
              <img :src="item.imgUrl" alt />
              <p>{{item.desc}}</p>
            </li>
          </ul>
        </van-swipe-item>
        <van-swipe-item>
          <ul class="u1">
            <li v-for="(item,key) in icon2" :key="key">
              <img :src="item.imgUrl" alt />
              <p>{{item.desc}}</p>
            </li>
          </ul>
        </van-swipe-item>
      </van-swipe>
      <!-- <ul class="u1">
        <li v-for="(item,key) in arr" :key="key">
          <img :src="item.imgUrl" alt />
          <p>{{item.desc}}</p>
        </li>
      </ul> -->
      <p class="p2">热销推荐</p>
      <div class="box2">
        <dl v-for="(item,key) in info" :key="key" @click="detail(item.id)">
          <dt>
            <img :src="item.imgUrl" alt />
          </dt>
          <dd>
            <p class="p3">{{item.title}}</p>
            <p class="p4">{{item.desc}}</p>
            <p class="p5">查看详情</p>
          </dd>
        </dl>
      </div>
      <p class="p2">周末去哪儿</p>
      <ul class="u2">
        <li v-for="(item,key) in list1" :key="key">
          <img :src="item.imgUrl" alt />
          <div class="box3">
            <p class="p6">{{item.title}}</p>
            <p class="p7">{{item.desc}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      value: "",
      list: [],
      list1: [],
      arr: [],
      info: []
    };
  },
  methods:{
    detail(id){
      this.$router.push('/detail?id='+id)
    }
  },
  mounted() {
    this.$http.get("/mock/index.json").then(res => {
      console.log(res);
      this.list = res.data.data.swiperList;
      this.arr = res.data.data.iconList;
      this.info = res.data.data.recommendList;
      this.list1 = res.data.data.weekendList;
    });
  },
  computed:{
    icon1(){
        return this.arr.filter(item => {
          return item.id != "0009";
          console.log(item.id);
        });
      },
      icon2(){
        return this.arr.filter(item => {
          return item.id == "0009";
          console.log(item.id);
        });
      }
  }
};
</script>
<style lang="scss" scoped>
header {
  width: 100%;
  height: 50px;
  background: #00c5c3;
  display: flex;
  .i {
    margin-top: 13px;
    font-size: 24px;
    color: #fff;
  }
}
.van-search {
  width: 310px;
}
.p1 {
  font-size: 16px;
  color: #fff;
  margin-top: 15px;
}
.my-swipe .van-swipe-item {
  color: #fff;
  font-size: 20px;
  text-align: center;
}
.box {
  height: 110px;
  img {
    height: 110px;
    width: 100%;
  }
}
.u1 {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  height: 187px;
  padding: 8px;
  li {
    margin-bottom: 8px;
    text-align: center;
    width: 21%;
    img {
      width: 59px;
      height: 59px;
      // margin: 0 11px;
    }
    p {
      font-size: 12px;
    }
  }
}
.p2 {
  font-size: 14px;
  background: #eee;
  padding: 5px 10px;
  // margin-bottom: 8px;
}
.box2 {
  padding: 0 8px;
}
dl {
  display: flex;
  font-size: 0;
  margin: 8px 0;
  dt {
    img {
      width: 80px;
      height: 80px;
    }
  }
  dd {
    margin-left: 8px;
  }
}
.p3 {
  font-size: 16px;
}
.p4 {
  font-size: 14px;
  color: #ccc;
  margin: 5px 0 8px 0;
}
.p5 {
  font-size: 14px;
  background: #ff9300;
  color: #fff;
  width: 70px;
  height: 22px;
  border-radius: 3px;
  text-align: center;
  line-height: 22px;
}
.u2 {
  font-size: 0;
  img {
    height: 130px;
    width: 100%;
  }
  .p6 {
    font-size: 16px;
    color: #333;
  }
  .p7 {
    font-size: 14px;
    color: #ccc;
  }
  .box3 {
    padding: 8px 8px;
  }
}
</style>
