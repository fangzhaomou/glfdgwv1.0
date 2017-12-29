<style lang="less" scoped>
  .BigPicture {
    width: 100%;
    max-width: 1200px;
    height: 400px;
    margin: 0 auto;
  }
  .swiper-container {
    background-color: #000;
  }
  .swiper-slide {
    background-size: cover;
    background-position: center;
  }
  .gallery-top {
    height: 80%!important;
    width: 100%;
  }
  .gallery-thumbs {
    height: 20%!important;
    box-sizing: border-box;
    padding: 10px 0;
  }
  .gallery-thumbs .swiper-slide {
    width: 25%;
    height: 100%;
    opacity: 0.4;
  }
  .gallery-thumbs .swiper-slide-active {
    opacity: 1;
  }
</style>

<template>
  <div class="BigPicture" ref="BigPicture" :style="{ height: height }">
      <!-- swiper1 -->
    <swiper :options="swiperOptionTop" class="gallery-top" ref="swiperTop">
      <swiper-slide class="slide" v-for="item in bigpicture" :style="{ backgroundImage: 'url(' + item.url + ')' }"></swiper-slide>
      <div class="swiper-button-next swiper-button-white" slot="button-next"></div>
      <div class="swiper-button-prev swiper-button-white" slot="button-prev"></div>
    </swiper>
    <!-- swiper2 Thumbs -->
    <swiper :options="swiperOptionThumbs" class="gallery-thumbs" ref="swiperThumbs">
      <swiper-slide class="slide" v-for="item in bigpicture" :style="{ backgroundImage: 'url(' + item.url + ')' }"></swiper-slide>
    </swiper>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        swiperOptionTop: {
          spaceBetween: 10,
          loop: true,
          loopedSlides: 4, //  looped slides should be the same
          autoplay: true,
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev'
          }
        },
        swiperOptionThumbs: {
          spaceBetween: 10,
          centeredSlides: true,
          slidesPerView: 'auto',
          touchRatio: 0.2,
          loop: true,
          loopedSlides: 4, //  looped slides should be the same
          autoplay: true,
          slideToClickedSlide: true
        },
        bigpicture: [
          {url: 'http://glfdgw.nos-eastchina1.126.net/tu3.png'},
          {url: 'http://glfdgw.nos-eastchina1.126.net/shuibeng2big.png'},
          {url: 'http://glfdgw.nos-eastchina1.126.net/glfdiot2.png'},
          {url: 'http://glfdgw.nos-eastchina1.126.net/alinkxbig.png'}
        ],
        height: '400px'
      }
    },
    // 监听器
    watch: {},
    //  计算属性
    computed: {},
    //  方法
    methods: {
    },
    //  组件
    components: {
    },
    //  初始化方法
    mounted: function () {
      //  2.32
      this.height = this.$refs.BigPicture.clientWidth / 2.32 + 'px'
      this.$nextTick(() => {
        const swiperTop = this.$refs.swiperTop.swiper
        const swiperThumbs = this.$refs.swiperThumbs.swiper
        swiperTop.controller.control = swiperThumbs
        swiperThumbs.controller.control = swiperTop
      })
    }
  }
</script>
