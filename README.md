# supermall2
?
## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).



=============================
❓❓❓
为什么伪元素after能清除浮动?
❓❓❓
data(){
  return{
    变量1:值,
    变量2:[],yi
  }
}
❓❓❓
创建组件时，新建index.js是为了导入方便???
//创建前
//引入
import Swiper from'common/swiper/Swiper.vue'
import SwiperItem from'common/swiper/SwiperItem.vue'
//创建后
// components/common/swiper/index.js
import Swiper from './Swiper'
import SwiperItem from './SwiperItem'
export{Swiper,SwiperItem}
//引入
import{Swiper,SwiperItem}from'common/swiper'
❓❓❓
v-for应该加什么key
为什么轮播图不滚动 要加key="index" 外层的swiper要加<swiper v-if="banners.length">

❓❓❓
父组件通过props将父组件种的数据传给子组件
父

❓❓❓
事件总线$bus