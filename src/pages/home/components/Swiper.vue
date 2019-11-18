<template>
  <div class="wrapper">
  <swiper :options="swiperOption" v-if="showSwiper">
    <swiper-slide
      v-for="item of list"
      :key="item.id"
    >
      <img class="swiper-img" :src="item.imgUrl">
    </swiper-slide>

    <div class="swiper-pagination"  slot="pagination"></div>
  </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeSwiper',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination'
        },
        loop: true,
        autoplay: {
          lazy: 2000
        }
      }
    }
  },
  computed: {
    showSwiper () {
      return this.list.length
    }
  }
}
</script>

<style scoped lang="stylus">
    /*样式穿透*/
  .wrapper >>> .swiper-pagination-bullet-active
    background-color #bbb !important
  .wrapper
    width 100%
    overflow hidden
    height 0
    padding-bottom 28.85%
   .swiper-img
     width 100%

</style>
