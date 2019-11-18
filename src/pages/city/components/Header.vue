<template>
  <div class="header">
  城市选择
    <router-link to="/">
    <div class="iconfont header-back">&#xe61e;</div>
    </router-link>
  </div>
</template>
<script>
export default {
  name: 'CityHeader'
}
</script>

<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .header
   position relative
   height $headerHeight
   line-height $headerHeight
   text-align center
   color #ffffff
   font-size .32rem
   background-color $bgColor
   .header-back
    position absolute
    top 0
    left 0
    width .64rem
    text-align center
    font-size .4rem
    color #ffffff

</style>
