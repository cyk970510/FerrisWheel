<template>
  <div id="app">
    <wheel />
    <swiper />
  </div>
</template>

<script>
import wheel from '@/page/wheel'
import swiper from '@/page/wheelSwiper'

export default {
  name: 'App',
  components: {
    wheel,
    swiper
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
