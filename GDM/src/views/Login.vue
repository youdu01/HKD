<template>
<div class="login">
    <el-form  ref="ruleForm" :model="loginForm" :rules="loginRules" class="login-form">
        <h3 class="title">若依后台管理系统</h3>
      <el-form-item prop="username">
        <el-input
          v-model="loginForm.username"
          type="text"
          auto-complete="off"
          placeholder="账号"
        >
          <el-icon></el-icon>
        </el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input
          v-model="loginForm.password"
          type="password"
          auto-complete="off"
          placeholder="密码"
          
        >
        <el-icon ></el-icon>
        </el-input>
      </el-form-item>
      <el-form-item >
      <el-form-item prop="code" v-if="captchaEnabled">
        <el-input
          v-model="loginForm.code"
          auto-complete="off"
          placeholder="验证码"
          style="width: 63%"
          
        />
      </el-form-item>
      <el-button
          :loading="loading"
         
          type="primary"
          style="width:100%;"
         
        >
          <span v-if="!loading">登 录</span>
          <span v-else>登 录 中...</span>
        </el-button>
        <div style="float: right;" v-if="register">
          <router-link class="link-type" :to="'/register'">立即注册</router-link>
        </div>
      </el-form-item>
    </el-form>
</div>
</template>
<script lang="ts" setup>
import { ref ,reactive} from "vue";
  const register = ref(false);
  const captchaEnabled = ref(false);
  const loading = ref(false);
  const loginRules = reactive({
      username: [
        { required: true, trigger: "blur", message: "请输入您的账号" },
      ],
      password: [
        { required: true, trigger: "blur", message: "请输入您的密码" },
      ],
      code: [
        { required: true, trigger: "change", message: "请输入验证码" },
      ],
    });
   const loginForm = reactive({
        username: "",
        password: "",
        rememberMe: false,
        code: "",
        uuid: ""
      }) 
</script>
<style scoped lang="scss">
.login {
  display: flex;
  justify-content: center;
  align-items: center;
 height: 100%;
background-color: #707070;
  background-size: cover;
}
.title {
  margin: 0px auto 30px auto;
  text-align: center;
  color: #707070;
}
.login-form {
  border-radius: 6px;
  background-color: #ffffff;
  width: 400px;
  padding: 25px 25px 5px 25px;
  .el-input {
    height: 38px;
    input {
      height: 38px;
    }
  }
  .input-icon {
    height: 39px;
    width: 14px;
    margin-left: 2px;
  }
}
.login-tip {
  font-size: 13px;
  text-align: center;
  color: #bfbfbf;
}
.login-code {
  width: 33%;
  height: 38px;
  float: right;
  img {
    cursor: pointer;
    vertical-align: middle;
  }
}
</style>