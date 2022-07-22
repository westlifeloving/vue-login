<template>
  <div class="login">
    <div class="login-container">
      <el-form
        :model="ruleForm2"
        :rules="rules2"
        status-icon
        ref="ruleForm2"
        label-position="left"
        label-width="0px"
        class="demo-ruleForm login-page"
        style="
          width: 280px;
          height: 280px;
          color: rgb(74, 74, 74);
          margin: 15% 0 0 35%;
        "
      >
        <h3 class="title" style="margin-left: 20%">精准访问控制登录</h3>
        <el-form-item prop="username">
          <el-input
            type="text"
            v-model="ruleForm2.username"
            auto-complete="off"
            placeholder="用户名"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input
            type="password"
            v-model="ruleForm2.password"
            auto-complete="off"
            placeholder="密码"
          ></el-input>
        </el-form-item>
        <el-checkbox
          v-model="checked"
          class="rememberme"
          style="margin: 0 0 20px 10px"
          >记住密码</el-checkbox
        >
        <el-form-item style="width: 100%">
          <el-button
            type="primary"
            style="width: 100%"
            @click="handleSubmit"
            :loading="logining"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      logining: false,
      ruleForm2: {
        username: "123",
        password: "456",
      },
      rules2: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" },
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
      },
      checked: false,
    };
  },
  methods: {
    // handleSubmit(){
    //     this.$refs.ruleForm2.validate((valid) => {
    //         if(valid){
    //             this.logining = true;
    //             if(this.ruleForm2.username === 'admin' &&
    //                this.ruleForm2.password === '123456'){
    //                    this.logining = false;s
    //                }
    //         }
    //     })
    // }
    handleSubmit() {
      this.$refs.ruleForm2.validate(async (valid) => {
        console.log(valid);
        if (!valid) return;
        const { data: res } = await this.$http.post("login", this.ruleForm2);
        console.log(res);
        if (res.meta.status != 200) return this.$message.error("登录失败");
        this.$message.success("登录成功");
      });
    },
  },
};
</script>

<style >
.login {
  background: linear-gradient(#b2f4f4, #53b2f9, #b3e9ff) !important;
  width: 100%;
  height: 100%;
  position: fixed;
  background-size: 100% 100%;
}
</style>
