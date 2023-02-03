<!-- 用户注册界面 -->
<template>
  <div id="login">
    <div class="bg"></div>
    <el-row class="main-container">
      <el-col :lg="8" :xs="16" :md="10" :span="10">
        <div class="top">
          <!-- <i class="iconfont icon-kaoshi"></i><span class="title">在线考试系统</span> -->
          <span class="title">用户注册</span>
        </div>
        <div class="bottom">
          <div class="container">
            <p class="title">请完善信息</p>
            <section class="add">
              <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="姓名">
                  <el-input v-model="form.studentName"></el-input>
                </el-form-item>
                <el-form-item label="性别">
                  <el-input v-model="form.sex"></el-input>
                </el-form-item>
                <el-form-item label="学院">
                  <el-input v-model="form.institute"></el-input>
                </el-form-item>
                <el-form-item label="所属专业">
                  <el-input v-model="form.major"></el-input>
                </el-form-item>
                <el-form-item label="年级">
                  <el-input v-model="form.grade"></el-input>
                </el-form-item>
                <el-form-item label="班级">
                  <el-input v-model="form.clazz"></el-input>
                </el-form-item>
                <el-form-item label="电话号码">
                  <el-input v-model="form.tel"></el-input>
                </el-form-item>
                <el-form-item label="身份证号">
                  <el-input v-model="form.cardId"></el-input>
                </el-form-item>
                <el-form-item label="邮箱">
                  <el-input v-model="form.email"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                  <el-input v-model="form.pwd"></el-input>
                </el-form-item>
                <el-form-item>
                  <el-button type="primary" @click="onSubmit()">立即创建</el-button>
                  <el-button type="text" @click="goback()">取消/goback</el-button>
                </el-form-item>
              </el-form>
            </section>
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row class="footer">
      <el-col>
        <p class="msg2">毕业设计</p>
      </el-col>
    </el-row>
    <!-- <section class="remind">
      <span>管理员账号：9527</span>
      <span>教师账号：20081001</span>
      <span>密码都是：123456</span>
    </section> -->
  </div>
</template>

<script>
import store from '@/vuex/store'
import {mapState} from 'vuex'
export default {
  store,
  name: "login",
  data() {
    return {
      form: { //表单数据初始化
        studentName: null,
        grade: null,
        major: null,
        clazz: null,
        institute: null,
        tel: null,
        email: null,
        pwd: null,
        cardId: null,
        sex: null,
        role: 2
      }
    }
  },
  methods: {
    onSubmit() { //数据提交
      this.$axios({
        url: '/api/student',
        method: 'post',
        data: {
          ...this.form
        }
      }).then(res => {
        if(res.data.code == 200) {
          this.$message({
            message: '数据添加成功',
            type: 'success'
          })
          this.$router.push({path: '/studentManage'})
        }
      })
    },
    cancel() { //取消按钮
      this.form = {}
    },
    goback() {
      this.$router.push({path: '/' }) //跳转到首页
    }
  },
  computed: mapState(["userInfo"]),
  mounted() {

  }
}
</script>

<style lang="scss" scoped>
.remind {
  border-radius: 4px;
  padding: 10px 20px;
  display: flex;
  position: fixed;
  right: 20px;
  bottom: 5%;
  flex-direction: column;
  color: #606266;
  background-color: #fff;
  border-left: 4px solid #409eff;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19)
}
.container {
  margin-bottom: 32px;
}
.container .el-radio-group {
  margin: 30px 0px;
}
a:link {
  color:#ff962a;
  text-decoration:none;
}
#login {
  font-size: 14px;
  color: #000;
  background-color: #fff;
}
#login .bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  overflow-y: auto;
  height: 100%;
  background: url('../../assets/img/loginbg1.jpeg') center top / cover no-repeat;
  background-color: #b6bccdd1 !important;
}
#login .main-container {
  display: flex;
  justify-content: center;
  align-items: center;
}
#login .main-container .top {
  margin-top: 100px;
  font-size: 30px;
  color: #ff962a;
  display: flex;
  justify-content: center;
}
#login .top .icon-kaoshi {
  font-size: 80px;
}
#login .top .title {
  margin-top: 20px;
  margin-bottom: 60px
}
#login .bottom {
  display:flex;
  justify-content: center;
  background-color:#fff;
  border-radius: 5px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#login .bottom .title {
  text-align: center;
  font-size: 30px;
}
.bottom .container .title {
  margin: 30px 0px;;
}
.bottom .submit .row-login {
  width: 100%;
  background-color: #04468b;
  border-color: #04468b;
  margin: 20px 0px 10px 0px;
  padding: 15px 20px;
}
.bottom .submit {
  display: flex;
  justify-content: center;
}
.footer {
  bottom: -50px;
  text-align: center;
}
.footer .msg1 {
  font-size: 18px;
  color: #fff;
  margin-bottom: 15px;
}
.footer .msg2 {
  font-size: 14px;
  color: #e3e3e3;
  margin-top: 70px;
}
.bottom .options {
  margin-bottom: 40px;
  color: #ff962a;
  display: flex;
  justify-content: space-between;
}
.bottom .options > a {
  color: #ff962a;
}
.bottom .options .register span:nth-child(1) {
  color: #8C8C8C;
}
.add {
  padding: 0px 40px;
  width: 400px;
}
</style>
