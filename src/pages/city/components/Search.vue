<template>
  <div>
    <div class="search">
      <input
        v-model="keyword"
        class="search-input"
        type="text"
        placeholder="请输入城市名或拼音">
    </div>
  <div
    class="search-content"
    ref="search"
    v-show="keyword"
  >
    <ul>
      <li
        class="search-item border-bottom"
        v-for="item of list"
        :key="item.id"
        @click="handleCityClick(item.name)"
      >{{item.name}}</li>
      <li class="search-item border-bottom" v-show="hasNOData">
         没有找到匹配数据
      </li>
    </ul>
  </div>
 </div>
</template>

<script>
import Bscroll from 'better-scroll'
import {mapMutations} from 'vuex'

export default {
  name: 'CitySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      keyword: '',
      list: [],
      timer: null
    }
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
  computed: {
    hasNOData () {
      return !this.list.length
    }
  },
  watch: {
    keyword () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.keyword) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const result = []
        for (let i in this.cities) {
          this.cities[i].forEach((value) => {
            if (value.spell.indexOf(this.keyword) > -1 ||
              value.name.indexOf(this.keyword) > -1) {
              result.push(value)
            }
          })
        }
        this.list = result
      }, 100)
    }
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.search)
  }
}
</script>

<style scoped lang="stylus">
  @import '~styles/varibles.styl'
  .search
    height .72rem
    padding 0 .1rem
    background-color $bgColor
    .search-input
      box-sizing border-box
      padding 0 .1rem
      height .62rem
      line-height .62rem
      width 100%
      text-align center
      border-radius 0.06rem
      color #666
  .search-content
   background-color #eee
   z-index 1
   overflow hidden
   position absolute
   top 1.58rem
   left 0
   right 0
   bottom 0
   .search-item
    line-height .62rem
    color #666
    padding-left .2rem
    background-color #ffffff
</style>
