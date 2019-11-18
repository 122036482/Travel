<template>
    <div class="header">
        <div class="header-left">
          <div class="iconfont back-icon">&#xe61e;</div>
        </div>

        <div class="header-input">
          <span class="iconfont search-icon">&#xe618;</span>
          输入城市/游玩/景点主题</div>
         <router-link to="/city">
        <div class="header-right">{{this.city}}

        <span class="iconfont">&#xe638;</span>

        </div>
         </router-link>
    </div>
</template>

<script>
import {mapState} from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .header
    display flex
    line-height $headerHeight
    background-color $bgColor
    color #ffffff
   .header-left
     width .64rem
     float left
     .back-icon
      font-size .4rem
      text-align center
   .header-input
     flex 1
     background-color #ffffff
     border-radius .1rem
     margin-top .12rem
     margin-left  .2rem
     height .64rem
     color #bbb
     padding-left .2rem
     line-height .64rem
   .header-right
     min-width: 1.04rem
     padding-left   0.1rem
     float: right
     line-height $headerHeight
     text-align  center
     color #fff
</style>
