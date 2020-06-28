<template xmlns="http://www.w3.org/1999/html">
   <div class="lg" @mousemove="moveBk">
     <img src="../assets/lg_bk.png" class="lg_bk" id="lg_bk" alt="">
     <img src="../assets/logo.png" alt="" class="logo">
     <div class="input_mes">
       <h1>友&nbsp;金</h1>
       <h2>您的私人理财顾问</h2>
       <el-input placeholder="请输入用户名" v-model="username" clearable></el-input>
       <el-input placeholder="请输入密码" v-model="psw" show-password></el-input>
       <div class="lg_bt"><div class="signup">注册</div><div class="signin" @click="check">登录</div></div>
      </div>
   </div>
</template>

<script>
export default {
   name: "Login",
   data () {
      return {
          username: '',
          psw: '',
      };
   },

   components: {},

   computed: {},
   mounted(){

   },
   methods: {
       moveBk(e){
           let bk = document.getElementById("lg_bk");
           bk.style.transform = 'translate('+(e.clientX-600)/10+'px,'+(e.clientY-300)/10+'px)';
       },
       check(){
           this.$router.push({path:'/home'})
       },
   }
}
</script>
<style>
  .lg{
    width: 100%;
    height: 100vh;
    overflow: hidden;
    position: relative;
  }
  .lg_bk{
    width: 120%;
    height: 120vh;
    transition: all 2s ease;
    position: absolute;
    top: -10%;
    left: -10%;
    z-index: -1;
    /*pointer-events: none;*/
  }
  .lg_bk:hover{
    transform: scale(1.2);
  }
  .input_mes{
    margin-top: 12vh;
    margin-left: 10%;
  }
  .input_mes .el-input__inner{
    background-color: rgba(0,0,0,0.4);
    color: rgba(255,255,255,0.8);
    border: none;
    height: 50px;
    margin-top: 20px;
    border-radius: 25px;
  }
  .input_mes .el-input--suffix{
    width: 30%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .input_mes h1{
    color: white;
    font-size: 6rem;
    margin-left: 10px;
  }
  .input_mes h2{
     color: #8D97A9;
     font-size: 2rem;
    margin-top: 10px;
    margin-left: 10px;
  }
  .logo{
    width: 4%;
    margin-left: 20px;
    margin-top: 20px;
  }
  .lg_bt{
    width: 80%;
    display: flex;
    margin-top: 20px;
  }
  .lg_bt div{
    width: 60px;
    height: 26px;
    border-radius: 13px;
    background-color: rgba(0,0,0,0.4);
    text-align: center;
    cursor: pointer;
    color: rgba(255,255,255,0.4);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .lg_bt div:hover{
    background-color: rgba(0,0,0,0.6);
    color: rgba(255,255,255,0.8);
  }
  .signup{
    margin-left: 10px;
  }
  .signin{
    margin-left: 20px;
  }
  .el-input__inner::placeholder {
    color: rgba(255,255,255,0.3);
  }
</style>
