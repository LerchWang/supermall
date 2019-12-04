<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control class="tab-control" @tabClick="tabClick"></tab-control>
    <good-list :goods="showGoodsList"></good-list>
    
  </div>
</template>

<script>
import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'
import GoodList from 'components/content/goods/GoodList'

import {getHomeMultidata, getHomeProductData} from 'network/home'

export default {
  name: 'Home',
  data() { 
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop':{page:1,list:[]},
        'new':{page:1,list:[]},
        'sell':{page:1,list:[]}
      },
      currentType: 'pop'
    }
  },
  props: {

  },
  computed:{
    showGoodsList(){
      return this.goods[this.currentType].list;
    }
  },
  components:{
    NavBar,
    HomeSwiper,
    RecommendView,
    FeatureView,
    TabControl,
    GoodList
  },
  created(){
    this._getHomeMultidata()

    this._getHomeProductData('pop')
    this._getHomeProductData('new')
    this._getHomeProductData('sell')
  },
  mounted() {

  },
  methods:{
    tabClick: function(index){
      switch(index) {
        case 0:
          this.currentType = "pop"
          break
        case 1:
          this.currentType = "new"
          break
        case 2:
          this.currentType = "sell"
          break
      }
    },

    _getHomeMultidata: function(){
      getHomeMultidata().then(res=>{
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    },
    _getHomeProductData: function(type){
      const page = this.goods[type].page
      getHomeProductData(type, page).then(res => {
        const newList = res.data.list
        this.goods[type].list.push(...newList)
        this.goods[type].page++
      })
    }
  },
  beforeCreate() {}, //生命周期 - 创建之前
  beforeMount() {}, //生命周期 - 挂载之前
  beforeUpdate() {}, //生命周期 - 更新之前
  updated() {}, //生命周期 - 更新之后
  beforeDestroy() {}, //生命周期 - 销毁之前
  destroyed() {}, //生命周期 - 销毁完成
  activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
 }
</script>

<style scoped>
#home {
  padding-top: 44px;
}

.home-nav {
  background-color: var(--color-tint);
  color: #fff;

  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
.tab-control {
  position: sticky;
  top: 44px;
  z-index: 9;
}
</style>