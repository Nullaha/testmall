<!--  -->
<template>
<div class="goods">
<goods-list-item v-for="(item,index) in goods" :key="index" 
                  :goodsItem="item"/>
</div>
</template>

<script>
import GoodsListItem from './GoodsListItem'

export default {
  name:"GoodsList",
  components:{
    GoodsListItem,
  },
  props:{
    goods:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style scoped>
/* 想在flex布局中一行设置两个怎么做？
  必须要有宽度，不然均等分的时候就往一行中塞 */
  .goods{
    display: flex;
    flex-wrap: wrap;
    /* 使得中间的空隙均等分 */
    justify-content: space-around;
    padding: 1px;
  }
  
  /* .good-item{
    flex: 1;
  } */
</style>