<template>
    <div class="list" ref="wrapper">
      <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
             <div class="button">{{this.currentCity}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
          <div class="button-list">
            <div
              class="button-wrapper"
              v-for="item of hot"
              :key="item.id"
              @click="handleCityClick(item.name)"
            >
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div
        class="area"
        v-for="(item,key) of cities"
        :key="key"
        :ref="key"
      >
        <div class="title border-topbottom">{{key}}</div>
        <div
          class="item-list"
          v-for="innerItem of item"
          :key="innerItem.id"
          @click="handleCityClick(innerItem.name)"
        >
          <div class="item border-bottom">{{innerItem.name}}</div>
        </div>
      </div>
    </div>
    </div>
</template>

<script>
import Bscroll from 'better-scroll'
import {mapState, mapMutations} from 'vuex'
export default {
  name: 'CityList',
  computed: {
    ...mapState({
      currentCity: 'city'
    })
  },
  props: {
    hot: Array,
    cities: Object,
    letter: String // 接收父组件传来的数据
  },
  methods: {
    handleCityClick (city) {
      // 把获取到的地址名称 传递到 vuex里保存
      // this.$store.commit('changeCity', city)
      this.changeCity(city)
      // 点击后返回到主页  也可以是你指定的页面
      // console.log(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper)
  },
  // 侦听器当letter改变时执行
  watch: {
    letter () {
      if (this.letter) {
        // 通过refs拿到对应的DOM
        const element = this.$refs[this.letter][0]
        // 利用scroll自带的api scrollToElement 跳转到指定的元素
        this.scroll.scrollToElement(element)
        // console.log(element)
      }
      // console.log(this.letter)
    }
  }
}
</script>

<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .border-topbottom
   &:before
     border-color #ccc
   &:after
    border-color #ccc
  .border-bottom
    &:before
     border-color #ccc
  .list
     position absolute
     top 1.58rem
     right 0
     bottom 0
     left 0
     overflow hidden
    .title
     font-size .26rem
     line-height .54rem
     background-color #eee
     padding-left .2rem
     color #666
    .button-list
     overflow hidden
     padding .1rem .6rem .1rem .1rem
     .button-wrapper
      width 33.33%
      float left
      .button
       text-align center
       margin 0.1rem
       padding 0.1rem 0
       border 0.02rem solid #ccc
       border-radius .1rem
    .item-list
     .item
      line-height .76rem
      padding-left .2rem
</style>
