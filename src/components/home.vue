<template>
  <div class="whole">
    <div class="menu">
      <img class="logo2" src="../assets/logo2.png" alt="">
      <ul class="menu_line">
        <li><i class="el-icon-house menu_icon"></i></li>
        <li><i class="el-icon-folder menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
      </ul>
    </div>
    <div class="main">
      <div class="header">
        <el-input placeholder="请输入内容" v-model="search_mes" clearable class="search_input"></el-input>
        <el-button type="primary" icon="el-icon-search" class="search_bt"></el-button>
      </div>
      <homeContent class="main_content"></homeContent>
    </div>
  </div>
</template>

<script>
  import homeContent from "./homeContent";
    export default {
        name: "home",
        components: {homeContent},
        data() {
            return {
                msg: "Hello Vue.js",
                search_mes: '',
            }
        },
        component: {
            homeContent,
        },
        mounted() {
        },
        method: {

        },

    }
</script>
<style>
  .whole{
    width: 100%;
    height: 100%;
    background-color: #2A2E31;
    display: flex;
  }
  .menu{
    width: 5%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .main{
    width: 95%;
    height: 100%;
    background-color: #F7F8FA;
    border-top-left-radius: 20px;
    border-bottom-left-radius: 20px;
  }
  .logo2{
    width: 50%;
    margin-top: 10px;
  }
  .menu_line{
    width: 100%;
    height: auto;
    margin-top: 10vh;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .menu_line li{
    width: 40px;
    height: 40px;
    background-color: #38393D;
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    margin-top: 20px;
  }
  .menu_icon{
    font-size: 20px;
    color: rgba(255,255,255,0.8);
  }
  .menu_line li:hover{
    background-color: white;
  }
  .menu_line li:hover .menu_icon{
    color: #2A2E31;
  }
  .header{
    width: 100%;
    height: 80px;
  }
  .search_input{
    width: 10%;
    line-height: 20px;
    margin-left: 10%;
    border: none;
    border-radius: 5px;
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
  }
  .main_content{
    width: 100%;
    height: auto;
  }
</style>
