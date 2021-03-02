<template>
  <div>
    <header>
      <div class="box">
        <p class="p1">城市选择</p>
        <van-icon name="arrow-left" class="i" @click="$router.go(-1)"/>
      </div>
      <van-search background="#00c5c3" placeholder="输入城市名或拼音" input-align="center"/>
    </header>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
header {
  background: #00c5c3;
  width: 100%;
  height: 90px;
}
.box {
  height: 40px;
  text-align: center;
  line-height: 40px;
  position: relative;
}
.p1 {
  font-size: 16px;
  color: #fff;
}
.i {
  position: absolute;
  top: 6px;
  left: 6px;
  color: #fff;
  font-size: 26px;
}
</style>