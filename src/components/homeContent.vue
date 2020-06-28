<template>
  <div class="main_content">
    <div class="home_left">
      <div class="header">
        <el-input placeholder="" v-model="search_mes" clearable class="search_input"></el-input>
        <el-button type="primary" icon="el-icon-search" class="search_bt"></el-button>
        <ul class="header_menu">
          <li class="header_li">中海石油</li>
          <li class="header_li">中海石油</li>
          <li class="header_li">中海石油</li>
          <li class="header_li">中海石油</li>
        </ul>
      </div>
      <div class="home_lt">
        <div class="home_lt1">
          <h2 class="content_title">折线图表</h2>
          <div class="home_content"></div>
        </div>
        <div class="home_lt2">
          <h2 class="content_title">折线图表</h2>
          <div class="home_content"></div>
        </div>
      </div>
      <div class="home_lb">
        <div class="home_lb_content">
          <h2 class="content_title">超长图表</h2>
          <div class="home_content"></div>
        </div>
      </div>
    </div>
    <div class="home_right">
      <el-calendar v-model="value" class="calendar">
      </el-calendar>
    </div>
  </div>
</template>

<script>
    export default {
        name: "homeContent",
        data() {
            return {
                msg: "Hello Vue.js",
                value: new Date(),
            }
        },
        component: {
            //someComponent
        },
        mounted() {
        },
        method: {

        },

    }
</script>

<style>
  .header{
    width: 100%;
    height: 80px;
    padding: 10px 10px;
  }
  .search_input{
    width: 20%;
    line-height: 20px;
    margin-left: 10%;
    border: none;
    border-radius: 5px;
    float: left;
  }
  .search_input .el-input__inner{
    line-height: 20px;
    height: 30px;
    padding: 0!important;
    border: none;
  }
  .search_bt{
    width: 30px;
    height: 30px;
    padding: 0;
    box-shadow: rgba(0,81,249,0.2) 5px 5px 10px;
    float: left;
  }
  .main_content{
    width: 100%;
    height: 100vh;
    display: flex;
  }
  .home_left{
    width: 70%;
    height: 100%;
    /*background-color: white;*/
  }
  .home_right{
    width: 30%;
    height: 100%;
    background-color: white;
    border-top-left-radius: 30px;
    border-bottom-left-radius: 30px;
    box-shadow: rgba(0,0,0,0.01) -5px 0px 20px;
  }
  .header_menu{
    float: left;
    display: flex;
    height: 30px;
    width: 50%;
    justify-content: space-around;
    margin-left: 10%;
    /*align-content: space-between;*/
  }
  .header_menu li{
    display: flex;
    justify-content: center;
    align-items: center;
    color: #B8BBC4;
    cursor: pointer;
    font-size: 16px;
    position: relative;
  }
  .header_li:hover{
    color: #2A2E31;
  }
  .header_li::before{
    width: 0px;
    height: 3px;
    position: absolute;
    bottom: 0px;
    background-color: #2A2E31;
    content: '';
    transition: all 0.2s linear;
  }
  .header_li:hover:before{
    width: 80%;
  }
  .home_lt{
    width: 100%;
    height: 46%;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }
  .home_lt1{
    width: 58%;
    height: 90%;
    /*overflow: hidden;*/
  }
  .home_lt2{
     width: 30%;
     height: 90%;
   }
  .home_lb{
    width: 100%;
    height: 40%;
    /*margin-top: 6px;*/
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .home_content{
    width: 100%;
    height: 90%;
    border-radius: 20px;
    background-color: white;
  }
  .content_title{
    margin-bottom: 20px;
    color: #2A2E31;
    font-size: 16px;
  }
  .home_lb_content{
    width: 92%;
    height: 200px;
  }
  .calendar{
    width: 90%;
    height: 100px;
  }
</style>
