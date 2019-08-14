<template>
  <div id="Register">
    <h1>用户注册</h1>
    <table id="registerTable">
      <tr>
        <td><label>用户名：</label></td>
        <td>
          <label><input type="text" id="AcctNo" maxlength="50"/></label>
          <span style="color:red">*</span>
        </td>
        <td><label>密码：</label></td>
        <td>
          <label><input type="text" id="PassWord" maxlength="50"/></label>
          <span style="color:red">*</span>
        </td>
      </tr>
      <tr>
        <td><label>真实姓名：</label></td>
        <td>
          <label><input type="text" id="actName" maxlength="50" /></label>
          <span style="color:red">*</span>
        </td>
        <td><label>联系电话：</label></td>
        <td>
          <label><input type="text" id="userPhone" maxlength="50" /></label>
          <span style="color:red">*</span>
        </td>
      </tr>
      <tr>
      <td><label>性别：</label></td>
      <td>
        <label><input type="text" id="userSex" maxlength="50" /></label>
      </td>
      <td><label>邮箱：</label></td>
      <td>
        <label><input type="text" id="userMail" maxlength="50" /></label>
      </td>
    </tr>
      <tr>
        <td><label>地址：</label></td>
        <td>
          <label><input type="text" id="userAddress" maxlength="50" /></label>
        </td>
        <td><label>id：</label></td>
        <td>
          <label><input type="text" id="userId" maxlength="50" /></label>
        </td>
      </tr>
    </table>
    <a>
      <button type="submit" v-on:click="_register"  style="margin-right:100px">注册 </button>
    </a>
    <router-link tag="a" :to="'/'">返回</router-link>
  </div>
</template>

<script>
export default {

  name: 'Register',

  data () {
    return {
      inputPrompt:""
    }
  },

  methods:{
      _register: function () {
          let user_accno = document.getElementById("AcctNo").value;
          let user_password = document.getElementById("PassWord").value;
          let user_name = document.getElementById("actName").value;
          let user_phone = document.getElementById("userPhone").value;
          if(!user_accno){alert("用户名不能为空");}
          else if(!user_password){alert("登录密码不能为空");}
          else if(!user_name){alert("真实姓名不能为空");}
          else if(!user_phone){alert("联系电话不能为空"); }
          else {
              axios.post('//user/addUser/', {
                  userId: document.getElementById("userId").value,
                  userName: user_accno,
                  userPhone: user_phone,
                  userRealName: user_name,
                  userMallName: document.getElementById("address").value,
                  userSex: document.getElementById("userSex").value,
                  userMail: document.getElementById("userMail").value,
                  userAddress: document.getElementById("userAddress").value
              })
              .then(function (response) {
                  console.log(response);
              })
              .catch(function (error) {
                  console.log(error);
              });

              axios.post('//user/addUser/', {
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
#MyInfo
  float center
</style>
