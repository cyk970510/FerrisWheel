<template>
  <section class="wheel">
    <section class="title">摩天轮</section>
    <section class="con">
      <section class="box">
        <section class="pic1">
          <img src="@/assets/1.png"/>
        </section>
        <section class="pic2">
          <img src="@/assets/2.png"/>
        </section>
        <section class="pic3">
          <img src="@/assets/3.png"/>
        </section>
      </section>
    </section>
  </section>
</template>

<script>
export default {
  name: 'wheel',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style scoped lang='scss'>
.wheel {
  position: relative;
  width: 100vw;
  height: 100vh;
  background-color: aqua;
  .title {
    position: absolute;
    top: 50%;
    left: 10vw;
    transform: translate(0, -50%);
    font-size: 1vw;
  }
  .box{
    position: absolute;
    top: 18vh;
    right: 17vw;
    width: 30vw;
    height: 30vw;
    animation: rotate 10s linear infinite;
    border: gray 1px dashed;
    border-radius: 50%;
    .pic1,.pic2,.pic3{
      width: 6.14vw;
      height: 6.14vw;
      position:absolute;
      animation:rotate1 10s linear infinite;
    }
    .pic1{
      top: 10vw;
      left: 25vw;
    }
    .pic2{
      top: 1vw;
      left: 0;
    }
    .pic3{
      top: 26vw;
      left: 12vw;
    }
  }
}
/*摩天轮的关键帧*/
@keyframes rotate{
  from { transform:rotate(0deg); }
  to { transform:rotate(360deg); }
}
/*三个小人的关键帧*/
@keyframes rotate1{
  from { transform:rotate(0deg); }
  to { transform:rotate(-360deg); }
}
</style>
