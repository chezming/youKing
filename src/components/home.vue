<template>
  <div class="whole">
    <div class="menu">
      <img class="logo2" src="../assets/logo2.png" alt="">
<!--      <div>{{this.$route.params.userid}}</div>-->
      <ul class="menu_line">
        <li :class="{active:act_menu === 0}" @click="changAct_menu(0)"><i class="el-icon-house menu_icon" :class="{active_icon:act_menu === 0}"></i></li>
        <li :class="{active:act_menu === 1}" @click="changAct_menu(1)"><i class="el-icon-folder menu_icon" :class="{active_icon:act_menu === 1}"></i></li>
        <li :class="{active:act_menu === 2}" @click="changAct_menu(2)"><i class="el-icon-reading menu_icon" :class="{active_icon:act_menu === 2}"></i></li>
        <li :class="{active:act_menu === 3}" @click="changAct_menu(3)"><i class="el-icon-data-line menu_icon" :class="{active_icon:act_menu === 3}"></i></li>
        <li :class="{active:act_menu === 4}" @click="changAct_menu(4)"><i class="el-icon-coin menu_icon" :class="{active_icon:act_menu === 4}"></i></li>
      </ul>
    </div>
      <homeContent class="main" v-if="act_menu === 0"></homeContent>
      <fund v-bind:userid="userid" class="main" v-if="act_menu === 1"></fund>
      <news class="main" v-if="act_menu === 2"></news>
  </div>
</template>

<script>
  import homeContent from "./homeContent";
  import news from "./news";
  import fund from "./fund";
    export default {
        name: "home",
        components: {
            homeContent,
            news,
            fund,
        },
        data() {
            return {
                msg: "Hello Vue.js",
                search_mes: '',
                act_menu: 0,
                userid:'',
            }
        },
        mounted() {
            this.userid = this.$route.params.userid;
        },
        methods: {
            changAct_menu(i){
                this.act_menu = i;
            }
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
