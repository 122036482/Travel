<template>
  <div class="container" @click="handleGallaryClick">
    <div class="wrapper">
      <swiper :options="swiperOption">
        <swiper-slide
        v-for="(item,index) of imgs"
        :key="index"
        >
          <img
            class="gallary-img"
            :src="item"
          />
        </swiper-slide>

        <div class="swiper-pagination" slot="pagination"></div>
      </swiper>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CommonGallary',
  props: {
    imgs: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
      swiperOption: {
        pagination: {
          el: '.swiper-pagination',
          type: 'fraction' //  分页器的类型
        },
        observer: true,
        observeParents: true
      }
    }
  },
  methods: {
    handleGallaryClick () {
      this.$emit('close')
    }
  }
}
</script>

<style scoped lang="stylus">
.container >>> .swiper-container
  overflow inherit
.container
  display flex
  flex-direction column
  justify-content center
  z-index 99
  position fixed
  left 0
  right 0
  top 0
  border-bottom 0
  background-color #000000
  height 100%
  .wrapper
   background-color #ffffff
   width 100%
   height 0
   padding-bottom 68.7%
   .gallary-img
     width 100%
   .swiper-pagination
    color #ffffff
    bottom -1rem
</style>
