<!--  -->
<template>

    <div class="wrapper">
      <ul class="content">
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
        <li>列表</li>
      </ul>
    </div>

</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: "Category",
  mounted(){
    new BScroll(document.querySelector('.content'))
  }
};
</script>

<style scoped>
  .wrapper {
    height: 150px;
    background-color: red;
    /* overflow: hidden;
    overflow-y: scroll; */
  }
</style>