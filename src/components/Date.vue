<template>
  <div class="date">
    <div class="header">
      <div class="left">left</div>
      <div class="center">2019年1月</div>
      <div class="right">right</div>
    </div>
    <div class="container">
      <div class="item" v-for="item in date">{{item}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Date",
    data(){
      return{
        date:['日','一','二','三','四','五','六']
      }
    }
  }
</script>

<style scoped lang="less">
.date{
  line-height: 1;
  .header{
    width: 6.5rem;
    padding: 0 .5rem;
    height: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /*background-color: #42b983;*/
    border-bottom: 1px solid #f5f5f5;
    background-color: #fff;
  }
  .container{
    background-color: #fff;
    width: 7rem;
    padding: .5rem .25rem;
    display: flex;
    flex-flow: row wrap;
    .item{
      height: .6rem;
      line-height: .6rem;
      text-align: center;
      width: 1rem;
    }
  }
}
</style>
