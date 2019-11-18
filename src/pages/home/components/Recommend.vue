<template>
    <div>
     <div class="title">热销推荐</div>
      <ul>
        <router-link
        tag="li"
        class="item border-bottom"
        v-for="item of list"
        :key="item.id"
        :to="'/detail/' + item.id"
        >

            <img class="item-img" :src="item.imgUrl">

           <div class="item-info">
             <p class="item-title">{{item.title}}</p>
             <p class="item-desc">{{item.desc}}</p>
             <button class="item-button">查看详情</button>
           </div>
        </router-link>
      </ul>

    </div>
</template>

<script>
export default {
  name: 'HomeRecommend',
  props: {
    list: Array
  }

}
</script>

<style scoped lang="stylus">
  @import "~styles/mixins.styl"
.title
  line-height .8rem
  text-indent .2rem
  background-color #eee
  margin-top .2rem
 .item
  overflow hidden
  display flex
  height 1.9rem
  .item-img
   width 1.7rem
   height 1.7rem
   padding .1rem
  .item-info
    flex 1
    padding .1rem
    min-width 0
    .item-title
     line-height .54rem
     font-size .32rem
     ellipses()
    .item-desc
      line-height .4rem
      color #ccc
      ellipses()
    .item-button
     margin-top .2rem
     background-color #ff9300
     padding 0 .2rem
     border-right: .6rem
</style>
