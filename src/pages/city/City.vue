<template>
  <div>
  <city-header></city-header>
  <city-search
    :cities="cities"
  ></city-search>
  <city-list
    :cities="cities"
    :hot="hotCities"
    :letter="letter"
  ></city-list>
  <city-alphabet
    :cities="cities"
    @change="handleLetterChange"
  ></city-alphabet>
  </div>
</template>
<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CitySearch from './components/Search'
import CityList from './components/List'
import CityAlphabet from './components/Alphabet'
export default {
  name: 'City',
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      // console.log(res)
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    // 接收子组件传递过来的数据
    handleLetterChange (letter) {
      // console.log(letter)
      // 把接收到子子组件传来的值 赋给 letter 然后在传递给他的兄弟组件
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>

<style scoped lang="stylus">

</style>
