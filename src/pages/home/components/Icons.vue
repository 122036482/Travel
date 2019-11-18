<template>
    <div class="icons">
      <swiper>
        <swiper-slide v-for="(page,index) of pages" :key="index">
        <div
            class="icon"
            v-for="item of page"
            :key="item.id"
        >
        <div class="icon-img">
        <img class="icon-imgcontent" :src="item.imgUrl">
        </div>
        <p class="icon-desc">{{item.desc}}</p>
      </div>
        </swiper-slide>
      </swiper>
    </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  computed: {
    // 计算
    // 根据数据项的不同自动化的构建页码
    pages () {
      const pages = []
      // 循环遍历数据线
      this.list.forEach((item, index) => {
        // 页码数
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }

}
</script>

<style scoped lang="stylus">
  @import "~styles/varibles.styl"
  @import "~styles/mixins.styl"

  .icons >>> .swiper-container
    height 0
    padding-bottom 50%
  .icons
   margin-top .1rem
  .icon
    position relative
    overflow hidden
    float left
    width 25%
    height 0
    padding-bottom 25%
    /*background-color red*/
    .icon-img
     position absolute
     top 0
     left 0
     right 0
     bottom 0.44rem
     box-sizing border-box
     padding .1rem
     /*background-color blue*/
     .icon-imgcontent
        width 100%
        display block
        margin 0 auto
        height 100%
   .icon-desc
    position absolute
    left 0
    right 0
    bottom 0
    line-height .44rem
    height .44rem
    text-align center
    color $darkTextColor
    ellipses()

</style>
