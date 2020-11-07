<template>
  <section class="swiper">
    <section class="title">摩天轮修改轮播</section>
    <section class="product__swiper" :style="{transform: `rotate(${roundSwiper}deg)`}">
      <section class="round round0" :style="{transform: `rotate(${roundItemDegArr[0]}deg)`}">
        <section class="swiper__item swiper__img0 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[0]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 0, 'swiper__curful': roundSwiperIndex === 1 || roundSwiperIndex === 6}" src="@/assets/1.png" alt="">
        </section>
      </section>
      <section class="round round1" :style="{transform: `rotate(${roundItemDegArr[1]}deg)`}">
        <section class="swiper__item swiper__img1 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[1]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 1, 'swiper__curful': Math.abs(roundSwiperIndex - 1) === 1}" src="@/assets/2.png" alt="">
        </section>
      </section>
      <section class="round round2" :style="{transform: `rotate(${roundItemDegArr[2]}deg)`}">
        <section class="swiper__item swiper__img2 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[2]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 2, 'swiper__curful': Math.abs(roundSwiperIndex - 2) === 1}" src="@/assets/3.png" alt="">
        </section>
      </section>
      <section class="round round3" :style="{transform: `rotate(${roundItemDegArr[3]}deg)`}">
        <section class="swiper__item swiper__img3 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[3]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 3, 'swiper__curful': Math.abs(roundSwiperIndex - 3) === 1}" src="@/assets/4.png" alt="">
        </section>
      </section>
      <section class="round round4" :style="{transform: `rotate(${roundItemDegArr[4]}deg)`}">
        <section class="swiper__item swiper__img4 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[4]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 4, 'swiper__curful': Math.abs(roundSwiperIndex - 4) === 1}" src="@/assets/5.png" alt="">
        </section>
      </section>
      <section class="round round5" :style="{transform: `rotate(${roundItemDegArr[5]}deg)`}">
        <section class="swiper__item swiper__img5 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[5]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 5, 'swiper__curful': Math.abs(roundSwiperIndex - 5) === 1}" src="@/assets/6.png" alt="">
        </section>
      </section>
      <section class="round round6" :style="{transform: `rotate(${roundItemDegArr[6]}deg)`}">
        <section class="swiper__item swiper__img6 cursor-hand" :style="{transform: `rotate(${-roundItemDegArr[6]}deg)`}">
          <img :class="{'swiper__cur': roundSwiperIndex === 6, 'swiper__curful': roundSwiperIndex === 0 || roundSwiperIndex === 5}" src="@/assets/7.png" alt="">
        </section>
      </section>
      <section class="roundHover">
        <section :class="['roundHover__common', `roundHover__${index}`]" v-for="(item, index) of 7" :key="index" @click="handleRound(index)"></section>
      </section>
      <section class="roundHover__s"></section>
    </section>
  </section>
</template>

<script>
export default {
  name: 'swiper',
  data () {
    return {
      roundFlag: null,
      roundSwiper: 0, // 旋转角度
      roundItemDegArr: [0, -80, -120, -160, -200, -240, -280],
      roundSwiperIndex: 0,
      roundChangeOpa: false,
      pageShowTransition: [false, false, false, false, false]
    }
  },
  mounted () {
    this.roundStart()
    const that = this
    document.addEventListener('visibilitychange', function () {
      if (document.visibilityState === 'hidden') {
        if (that.pageIndex === 2) {
          clearInterval(that.roundFlag)
        }
      } else {
        if (that.pageIndex === 2) {
          clearInterval(that.roundFlag)
          that.roundStart()
        }
      }
    })
  },
  methods: {
    handleRound (index) {
      if (index === 0) return
      clearInterval(this.roundFlag)
      this.roundChangeOpa = true
      setTimeout(() => {
        this.roundChangeOpa = false
      }, 600)
      let arr = [0, 1, 2, 3, 4, 5, 6]
      arr.splice(this.roundSwiperIndex, 1)
      let sortArr = arr.slice(this.roundSwiperIndex).concat(arr.slice(0, this.roundSwiperIndex))
      if (index <= 3) {
        // 逆时针
        while (index > 0) {
          for (let j = 0; j < sortArr.length; j++) {
            this.roundItemDegArr[sortArr[j]] += 40
          }
          this.roundItemDegArr[sortArr[0]] += 40
          this.roundItemDegArr[this.roundSwiperIndex] += 80
          if (this.roundSwiperIndex === 6) {
            this.roundSwiperIndex = 0
          } else {
            this.roundSwiperIndex++
          }
          let arr1 = [0, 1, 2, 3, 4, 5, 6]
          arr1.splice(this.roundSwiperIndex, 1)
          sortArr = arr1.slice(this.roundSwiperIndex).concat(arr1.slice(0, this.roundSwiperIndex))
          index--
        }
        this.roundStart()
      } else {
        // 顺时针
        while (index < 7) {
          for (let j = 0; j < sortArr.length; j++) {
            this.roundItemDegArr[sortArr[j]] -= 40
          }
          this.roundItemDegArr[sortArr[5]] -= 40
          this.roundItemDegArr[this.roundSwiperIndex] -= 80
          if (this.roundSwiperIndex === 0) {
            this.roundSwiperIndex = 6
          } else {
            this.roundSwiperIndex--
          }
          let arr1 = [0, 1, 2, 3, 4, 5, 6]
          arr1.splice(this.roundSwiperIndex, 1)
          sortArr = arr1.slice(this.roundSwiperIndex).concat(arr1.slice(0, this.roundSwiperIndex))
          index++
        }
      }
    },
    roundStart () {
      this.roundFlag = setInterval(() => {
        this.roundChangeOpa = true
        setTimeout(() => {
          this.roundChangeOpa = false
        }, 600)
        if (this.roundSwiperIndex === 6) {
          this.roundSwiperIndex = 0
        } else {
          this.roundSwiperIndex++
        }
        for (let i = 0; i < this.roundItemDegArr.length; i++) {
          this.roundItemDegArr[i] += 40
          if (i === this.roundSwiperIndex && i === 0) {
            this.roundItemDegArr[0] += 40
            this.roundItemDegArr[6] += 40
          } else if (i === this.roundSwiperIndex && i !== 0) {
            this.roundItemDegArr[i] += 40
            this.roundItemDegArr[i - 1] += 40
          }
        }
      }, 4000)
    }
  }
}
</script>

<style scoped lang='scss'>
.swiper {
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
  .product__swiper {
    position: absolute;
    top: 18vh;
    right: 17vw;
    width: 33.18vw;
    height: 33.18vw;
    border-radius: 50%;
    border: gray 1px dashed;
    transition: all 1s;
    .round {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border-radius: 50%;
      transition: all 1s;
      background: transparent;
      border: none;
      .swiper__item {
        position: absolute;
        top: 68%;
        left: 0;
        width: 6.14vw;
        height: 6.14vw;
        transition: all 1s;
        z-index: 100;
        img {
          width: 100%;
          height: 100%;
        }
        .swiper__cur {
          transform: scale(2.4);
        }
        .swiper__curful {
          transform: scale(1.3);
        }
      }
      .swiper__img0 {
        top: 68%;
        left: 0;
        transform: rotate(60deg);
      }
      img {
        border-radius: 10%;
        transition: all 1s;
      }
    }
    .roundHover {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background: transparent;
      border: none;
      z-index: 150;
      background-color: transparent;
      &__common {
        position: absolute;
        width: 6.14vw;
        height: 6.14vw;
        border-radius: 10%;
        background-color: transparent;
      }
      &__common:hover {
        cursor: pointer;
      }
      &__0 {
        top: 68%;
        transform: scale(2.4);
      }
      &__1 {
        left: 60.5%;
        top: 86%;
        transform: scale(1.3);
      }
      &__2 {
        left: 85%;
        top: 62.5%;
      }
      &__3 {
        left: 88.5%;
        top: 29.1%;
      }
      &__4 {
        left: 70%;
        top: 1.2%;
      }
      &__5 {
        left: 38%;
        top: -8%;
      }
      &__6 {
        left: 7%;
        top: 5.5%;
        transform: scale(1.3);
      }
    }
    .roundHover__s {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 40%;
      height: 40%;
      border-radius: 50%;
      background: transparent;
      border: gray 1px dashed;
      z-index: 149;
      background-color: transparent;
    }
  }
}
</style>
