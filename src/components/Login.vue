<template xmlns="http://www.w3.org/1999/html">
   <div class="lg" @mousemove="moveBk">
     <img src="../assets/lg_bk.png" class="lg_bk" id="lg_bk" alt="">
     <img src="../assets/logo.png" alt="" class="logo">
     <div class="input_mes">
       <h1>友&nbsp;金</h1>
       <h2>您的私人理财顾问</h2>
       <el-input placeholder="请输入用户名" v-model="userid" clearable></el-input>
       <el-input placeholder="请输入密码" v-model="psw" show-password></el-input>
       <div class="lg_bt"><div class="signup" @click="signup">注册</div><div class="signin" @click="check">登录</div></div>
      </div>
     <el-dialog :title="'注册用户'" :visible.sync="dialogVisible" width="30%"  :before-close="handleClose">
       <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
         <el-form-item label="账号" prop="id">
           <el-input v-model="ruleForm.id"></el-input>
         </el-form-item>
         <el-form-item label="姓名" prop="name">
           <el-input v-model="ruleForm.name"></el-input>
         </el-form-item>
         <el-form-item label="性别" prop="sex">
           <el-radio-group v-model="ruleForm.sex">
             <el-radio label="男"></el-radio>
             <el-radio label="女"></el-radio>
           </el-radio-group>
         </el-form-item>
         <el-form-item label="年龄" prop="age">
           <el-input type="text" v-model="ruleForm.age"></el-input>
         </el-form-item>
         <el-form-item label="密码" prop="psw">
           <el-input type="password" v-model="ruleForm.psw" minlength="10"></el-input>
         </el-form-item>
         <el-form-item label="确认密码" prop="psw2">
           <el-input type="password" v-model="ruleForm.psw2"></el-input>
         </el-form-item>
         <el-form-item>
           <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
           <el-button @click="resetForm('ruleForm')">重置</el-button>
           <el-button @click="cancellForm('ruleForm')">取 消</el-button>
         </el-form-item>
       </el-form>
       <span slot="footer" class="dialog-footer">
<!--    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>-->
      </span>
     </el-dialog>
   </div>
</template>

<script>
import axios from 'axios';
export default {
   name: "Login",
   data () {
      return {
          userid: '',
          psw: '',
          dialogVisible: false,
          link: 'http://localhost:8181',
          ruleForm:{
              id: '',
              sex: '',
              name: '',
              age: null,
              psw: '',
              psw2: '',
          },
          investor:{
              investorid: '',
              investorsex: '',
              investorname: '',
              investorage: null,
              investorpsd: '',
          },
          rules: {
              id: [
                  {required: true, message: '请输入id账号', trigger: 'blur'},
                  {min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur'}
              ],
              age: [
                  {required: true, message: '请输入年龄', trigger: 'blur'}
              ],
              name: [
                  {required: true, message: '请输入姓名', trigger: 'blur'}
              ],
              sex: [
                  {required: true, message: '请选择性别', trigger: 'change'}
              ],
              psw: [
                  {required: true, message: '密码', trigger: 'blur'}
              ],
              psw2: [
                  {required: true, message: '密码不符', trigger: 'blur'}, {
                      validator: (rule, value, callback) => {
                          if (value === '') {
                              callback(new Error('请再次输入密码'))
                          } else if (value !== this.ruleForm.psw) {
                              callback(new Error('两次输入密码不一致'))
                          } else {
                              callback()
                          }
                      }
                  }
              ],

          },
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
           axios.get(this.link+'/inv_basis/signin/'+this.userid+'/'+this.psw).then(res =>{
               if(res.data === ""){
                   console.log('获取数据失败');
                   alert('账号或密码错误!');
               }else {
                   alert('登录成功!');
                   console.log(res);
                   this.$router.push({name:'home', params: { userid: this.userid }});
               }
           }).catch((e) => {
               console.log('获取数据失败');
               alert('账号或密码错误!');
           });
       },
       signup(){
           this.dialogVisible = true;
       },
       submitForm(formName){
           this.investor.investorid = this.ruleForm.id;
           this.investor.investorsex = this.ruleForm.sex;
           this.investor.investorname = this.ruleForm.name;
           this.investor.investorage = this.ruleForm.age;
           this.investor.investorpsd = this.ruleForm.psw;
           console.log(this.investor);
           let _this = this;
           this.$refs[formName].validate((valid) => {
               if (valid) {
                   axios.post(this.link+'/inv_basis/signup',this.investor).then(res =>{
                       alert('注册成功!');
                       _this.dialogVisible = false;
                       this.$refs[formName].resetFields();
                       console.log(res);
                   })
               } else {
                   console.log('信息错误');
                   return false;
               }
           });
       },
       resetForm(formName) {
           this.$refs[formName].resetFields();
       },
       cancellForm(formName) {
           this.$refs[formName].resetFields();
           this.dialogVisible=false;
       },
       handleClose(){
           this.cancellForm('ruleForm');
       }
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
