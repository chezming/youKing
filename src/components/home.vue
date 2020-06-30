<template>
  <div class="whole">
    <div class="menu">
      <img class="logo2" src="../assets/logo2.png" alt="">
      <ul class="menu_line">
        <li :class="{active:act_menu === 0}"><i class="el-icon-house menu_icon" :class="{active_icon:act_menu === 0}"></i></li>
        <li><i class="el-icon-folder menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
        <li><i class="el-icon-house menu_icon"></i></li>
      </ul>
    </div>n
      <homeContent class="main"></homeContent>
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
                act_menu: 0,
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
    border-top-left-radius: 30px;
    border-bottom-left-radius: 30px;
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
  .active{
    background-color: white!important;
  }
  .active_icon{
    color: #2A2E31;
  }
</style>
