<template>
  <div id="Register">
    <h1>用户注册</h1>
    <table class="registerTable">

      <tr>
        <td><label>用户名：</label></td>
        <td class="registerShow">
          <label><input type="text" id="AcctNo" maxlength="30" v-model="user_name" @input="_inputUsername" @click="_inputUsername"/></label>
          <span style="color:red">*</span>
        </td>
        <td><label>密码：</label></td>
        <td class="registerShow">
          <label><input type="text" id="PassWord" maxlength="12" v-model="user_password" @input="_inputPassword" @click="_inputPassword"/></label>
          <span style="color:red">*</span>
        </td>
      </tr>
      <tr>
          <td>&nbsp</td>
          <td class="promptText">{{usernamePrompt}}</td>
          <td>&nbsp</td>
          <td class="promptText">{{passwordPrompt}}</td>
      </tr>

      <tr>
        <td><label>邮箱：</label></td>
        <td class="registerShow">
          <label><input type="text" id="userMail" maxlength="50" @change="_inputMail"/></label>
          <span style="color:red">*</span>
        </td>
        <td><label>联系电话：</label></td>
        <td class="registerShow">
          <label><input type="tel" onkeyup="value=value.replace(/[^\d]/g,'')" id="userPhone" @click="_inputPhone"/></label>
          <span style="color:red">*</span>
        </td>
      </tr>
       <tr>
          <td>&nbsp</td>
          <td class="promptText">{{mailPrompt}}</td>
          <td>&nbsp</td>
          <td class="promptText">{{phonePrompt}}</td>
       </tr>

      <tr>
          <td><label>姓名：</label></td>
          <td class="registerShow">
            <label><input type="text" id="actName" maxlength="50" /></label>
          </td>
          <td><label>性别：</label></td>
          <td class="registerShow">
              <select style="width:50px">
                  <option value="male">男</option>
                  <option value="female">女</option>
              </select>
          </td>
      </tr>
        <tr>
            <td>&nbsp</td>
            <td>&nbsp</td>
            <td>&nbsp</td>
            <td>&nbsp</td>
        </tr>

        <tr>
        <td><label>地址：</label></td>
        <td class="registerShow">
          <label><input type="text" id="userAddress" maxlength="50" /></label>
        </td>
        <td><label>id：</label></td>
        <td class="registerShow">
          <label><input type="text" id="userId" maxlength="50" /></label>
        </td>
      </tr>

    </table>
      <br/>
      <br/>
    <a>
      <button type="submit" v-on:click="_register" style="margin-right:100px">注册 </button>
    </a>
    <router-link tag="a" :to="'/'">返回</router-link>
  </div>
</template>

<script>

    import axios from "axios";

    export default {

      name: 'Register',

      data () {
        return {
          user_name:"",
          user_password:"",

          usernamePrompt:"",
          passwordPrompt:"",
          phonePrompt:"",
          mailPrompt:""
        }
      },

      methods:{

          checkUserName(){
              return this.user_name === this.user_name.replace(/[^\d\a-zA-Z]/gi,'');
          },

          checkPassword(){
              return this.user_password === this.user_password.replace(/[^\d\a-zA-Z]/gi,'');
          },

          _inputUsername: function(){
            if(!this.checkUserName()) {
               this.usernamePrompt = "用户名只能为数字和字母的组合";
               this.user_name = this.user_name.replace(/[^\d\a-zA-Z]/gi,'');
            }else {
               this.usernamePrompt = "";
            }
          },

          _inputPassword: function(){
              if(!this.checkPassword()) {
                  this.passwordPrompt = "用户名只能为数字和字母的组合";
                  this.user_password = this.user_password.replace(/[^\d\a-zA-Z]/gi,'');
              }else {
                  this.passwordPrompt = "";
              }
          },

          _inputPhone: function(){
              this.phonePrompt = "";
          },

          _inputMail: function(){
              this.mailPrompt = "";
          },


          _register: function () {
              let user_acct = document.getElementById("AcctNo").value;
              let user_password = document.getElementById("PassWord").value;
              let user_mail = document.getElementById("userMail").value;
              let user_phone = document.getElementById("userPhone").value;

              if(!user_acct){
                  this.usernamePrompt = "用户名不能为空";
              } else if(!user_password){
                  this.passwordPrompt = "密码不能为空";
              } else if(!this.checkPassword()){
                  this.passwordPrompt = "用户名只能为数字和字母的组合";
              } else if(!user_mail){
                  this.mailPrompt = "邮箱不能为空";
              } else if(!user_phone){
                  this.phonePrompt = "手机号不能为空";
              } else if(user_phone.length !== 11){
                  this.phonePrompt = "请输入正确的手机号";
              } else{
                  axios.post('/user/addUser/', {
                      userId: document.getElementById("userId").value,
                      userName: user_acct,
                      userPhone: user_phone,
                      userRealName: document.getElementById("actName").value,
                      userMallName: document.getElementById("address").value,
                      userSex: document.getElementById("userSex").value,
                      userMail: user_mail,
                      userAddress: document.getElementById("userAddress").value
                  })
                  .then(function (response) {
                      console.log(response);
                  })
                  .catch(function (error) {
                      console.log(error);
                  });

                  axios.post('/user/addUser/', {
                      userId: document.getElementById("userId").value,
                      userName: document.getElementById("ActName").value,
                      userPassword: user_password
                  })
                  .then(function (response) {
                      console.log(response);
                  })
                  .catch(function (error) {
                      console.log(error);
                  });
              }
          }
      }
    };
</script>



<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
  #Register
     float center
  .registerTable
     height 20px
     text-align right
  .registerShow
     width 200px
     text-align left
  .promptText
     text-align left
     color red
</style>
