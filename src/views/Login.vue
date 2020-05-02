<template>
  <div>
    <div class="container">
      <el-form :model="ruleForm"  status-icon ref="ruleForm" class="demo-ruleForm">
        <el-form-item prop="name">
          <el-input type="password"  maxlength=10 placeholder="请输入账号" v-model="ruleForm.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item prop="pass">
          <el-input type="password" maxlength=10 show-password	 placeholder="请输入密码" v-model="ruleForm.pass" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item style="margin-left:20px">
          <el-radio-group v-model="ruleForm.role" size="medium">
            <el-radio border label="student">学生</el-radio>
            <el-radio border label="teacher">老师</el-radio>
            <el-radio border label="admin">管理</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item style="margin-bottom:40px">
          <div class="submit-btn">
            <el-button type="primary" @click="submitForm(ruleForm)">登录</el-button>
          </div>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import url from "@/service.config.js";
export default {
  data() {
    return {
      uasername: "",
      password: "",
      radio: "student",
      ruleForm: {
        name: "",
        pass: "",
        role: "student"
      }
    };
  },
  methods: {
    submitForm(e) {
      let flag = true;
      if (e.name == "") {
        console.log('name=="');
      }
      if (e.pass == "") {
        console.log('pass == "');
      }
      if (flag) {
        console.log(e.name);
        console.log(e.pass);
        console.log(e.role);
      }
    axios({
        url:url.login,
        method:'post',
        data:{
            userName:this.ruleForm.name,
            password:this.ruleForm.pass,
            role:this.ruleForm.role
        }
    }).then(res=>{
        if(res.data.code == 200){
            console.log('成功')
        }
        console.log(res)
    })
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  padding: 40px 40px 20px 40px;
  border: 1px solid rgba($color: #ddd, $alpha: 0.4);
  width: 400px;
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translateX(-50%);
}
.submit-btn {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
</style>