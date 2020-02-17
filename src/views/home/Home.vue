<!--  -->
<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <tab-control :titles="['流行','新款','精选']" @tabClick="tabClick" class="tab-control"  v-show="isTabFixed" ref="tabControl1"></tab-control>
    <scroll class="content" ref="scroll" 
            :probe-type="3" @scroll="contentScroll" 
            :pull-up-load='true' @pullingUp="loadMore">
      <home-swiper :banners="banners" @swiperImageLoad="swiperImageLoad"></home-swiper>
      <home-recommend-view :recommends="recommends"></home-recommend-view>
      <home-feature-view></home-feature-view>
      <tab-control :titles="['流行','新款','精选']" @tabClick="tabClick"  ref="tabControl2"></tab-control>
      <goods-list :goods="showGoods"></goods-list>
    </scroll>

    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
// 子组件
import HomeSwiper from "./childComps/HomeSwiper";
import HomeRecommendView from "./childComps/HomeRecommendView";
import HomeFeatureView from "./childComps/HomeFeatureView";
// 公共组件
import NavBar from "components/common/navbar/NavBar.vue";
import TabControl from "components/content/tabControl/TabControl.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
import Scroll from "components/common/scroll/Scroll.vue";
import BackTop from 'components/content/backTop/BackTop.vue'
// 其他
import { getHomeMultidata, getHomeGoods } from "network/home";
import {debounce} from 'common/utils.js';

export default {
  name: "Home",
  components: {
    HomeSwiper,
    HomeRecommendView,
    HomeFeatureView,
    NavBar,
    TabControl,
    GoodsList,
    Scroll,
    BackTop,
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currentType: "pop",
      isShowBackTop:false,
      tabOfffsetTop:0,
      isTabFixed:false,
      saveY:0,
    };
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    }
  },
  destroyed(){
    console.log('home destroyed');
  },
  activated(){
    console.log('activated');
    this.$refs.scroll.refresh();
    this.$refs.scroll.scrollTo(0,this.saveY,0)
    this.$refs.scroll.refresh();
  },
  deactivated(){
    console.log('deactivated');
    // this.saveY=-1000;
    console.log(this.saveY);
    
    this.saveY=this.$refs.scroll.getScrollY();
    
  },
  created() {
    //1请求多个数据
    this.getHomeMultidata();
    // 2请求商品数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");

  },
  mounted(){
    
    //1图片加载完成的事件监听(防抖)
    const refresh=debounce(this.$refs.scroll.refresh,500)
    this.$bus.$on('itemImageLoad',()=>{
      // console.log('----');
      // this.$refs.scroll.refresh();
      refresh()
    })
    
  },
  beforeDestroy(){
    this.$bus.$off('itemImageLoad');
  },
  methods: {
    // 事件监听相关的方法
    
    tabClick(index) {
      // console.log(index);
      switch (index) {
        case 0:
          this.currentType = "pop";
          break;
        case 1:
          this.currentType = "new";
          break;
        case 2:
          this.currentType = "sell";
          break;
      }
      this.$refs.tabControl1.currentIndex=index;
      this.$refs.tabControl2.currentIndex=index;
    },
    backClick(){
      // console.log('点击了组件');
      this.$refs.scroll.scrollTo(0,0,500)
    },
    contentScroll(position){
      //1backTop是否显示
      this.isShowBackTop=(-position.y)>1000;
      //2 tabControl是否吸顶
      this.isTabFixed=(-position.y)>this.tabOffsetTop;
    },
    loadMore(){
      console.log('-----')
      this.getHomeGoods(this.currentType);//获取数据
      this.$refs.scroll.refresh();//进行一次刷新
    },
    swiperImageLoad(){
      //获取tabControl的offsetTop
      //所有的组件都有一个属性$el：用于获取组件中的元素
      this.tabOffsetTop=this.$refs.tabControl2.$el.offsetTop;
      // console.log(this.$refs.tabControl.$el.offsetTop);
    },
    // 网络请求相关的方法
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        console.log(res);
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        console.log(res);
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        this.$refs.scroll.finishPullUp() //上拉加载完成
      });
    }
  }
};
</script>

<style scoped>
#home {
  /* padding-top: 44px; */
  height: 100vh;
  position: relative;
}

.home-nav {
  background-color: var(--color-tint);
  color: #fff;
/* 
  在使用浏览器原生滚动时，为了导航不跟随一起滚动
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9; */
}

.content{
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;

}

.tab-control{
  position: relative;
  z-index: 9;
}

/* 
.content{
  height: calc(100% - 93px);
  overflow: hidden;
  margin-top: 44px;

} */
</style>