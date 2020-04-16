<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatart_box">
        <img src="../assets/logo.png"
             alt />
      </div>
      <!--登录表单区域-->
      <el-form class="login_form"
               :model="loginForm"
               :rules="loginFormRules"
               ref="loginFormRef">
        <!--账号-->
        <el-form-item prop="username">
          <el-input prefix-icon="el-icon-user-solid"
                    v-model="loginForm.username">
          </el-input>
        </el-form-item>
        <!--密码-->
        <el-form-item prop="password">
          <el-input prefix-icon="el-icon-s-goods"
                    v-model="loginForm.password"
                    type="password"></el-input>
        </el-form-item>
        <!-- 按钮区域 -->
        <el-form-item class="btns">
          <el-button type="primary"
                     @click="login">登录</el-button>
          <el-button type="info"
                     @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      loginFormRules: {
        username: [
          { required: true, message: '请输入登录账号', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入登录密码', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 6 到 8 个字符', trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    resetLoginForm() {
      this.$refs.loginFormRef.resetFields();
    },
    login() {
      this.$refs.loginFormRef.validate(validate => {
        console.log(validate);
        const result = this.$http.get('/api/v3/user/getList', {
          params: {
            type: 1, status: 2, pageNum: 1, pageSize: 20
          }
        });
        console.log(result);
      })
    }
  }
};
</script>

<style lang="less" scoped>
.login_container {
  background: #2b4b6b;
  height: 100%;
}
.login_box {
  background: #fff;
  height: 300px;
  width: 450px;
  border-radius: 5px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avatart_box {
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background: #fff;
  img {
    height: 100%;
    width: 100%;
    border-radius: 50%;
    background: #eee;
  }
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
.btns {
  display: flex;
  justify-content: flex-end;
}
</style>
