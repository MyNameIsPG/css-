<template>
  <div class="login-wrap" id="particlesDom">
    <div class="left-basemap-box">
      <img class="left-basemap" src="@/assets/img/login/left-base-map.png" alt />
      <div class="left-basemap-text fadeInDownBig animated">
        <!-- <p class="maintitle">苏台高速七都至桃源段一期工程</p>
        <p class="subtitle">苏台高速七都至桃源段一期工程</p> -->
        <p class="maintitle">重庆东站</p>
        <p class="subtitle">重庆东站</p>
      </div>
    </div>
    <div class="login-form">
      <div class="login-form-warp">
        <div class="login-form-warp-body">
          <!-- <div class="login-form-title">公路全过程数字化平台</div> -->
          <div class="login-form-title">工程建设全过程管理平台</div>
          <div class="form-group">
            <label class="form-group-label">
              <img src="@/assets/img/login/username.png" alt="账户" />
              <span>账户</span>
            </label>
            <div class="form-group-control">
              <input
                type="text"
                v-model="form.username"
                class="login_input"
                placeholder="请输入账户名"
              />
            </div>
          </div>
          <div class="form-group">
            <label class="form-group-label">
              <img src="@/assets/img/login/password.png" alt="密码" />
              <span>密码</span>
            </label>
            <div class="form-group-control">
              <input
                type="password"
                v-model="form.password"
                class="login_input"
                placeholder="请输入密码"
              />
            </div>
          </div>
        </div>
        <div class="login-form-warp-footer" @click="handelSubmit()">
          <button>
            <img class="cutter_head" src="@/assets/img/login/btn-icon.png" alt />
            <span class="login_text">登&nbsp;&nbsp;&nbsp;录</span>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import md5 from "js-md5";
import particlesConfig from "./particles.json";
import { resLoginApiCheckLogin } from "@/api";
import { IS_OK } from "@/api/path";
export default {
  name: "Login",
  data() {
    return {
      form: {
        username: "",
        password: "",
        verifycode: 1,
      },
    };
  },
  mounted(){
    this.init();
  },
  methods: {
    init() {
      window.particlesJS("particlesDom", particlesConfig);
    },
    handelSubmit() {
      this.$router.push({ path: "/projectSelect" });
      // if (!this.form.username) {
      //   this.$message({
      //     message: "请输入账号",
      //     type: "warning",
      //   });
      //   return false;
      // }
      // if (!this.form.password) {
      //   this.$message({
      //     message: "请输入密码",
      //     type: "warning",
      //   });
      //   return false;
      // }
      // let params = {
      //   username: this.form.username,
      //   password: md5(this.form.password),
      //   verifycode: this.form.verifycode,
      // };
      // this.submitData(params);
    },
    async submitData(params) {
      let loading = this.$loading({
        lock: true,
        text: "正在登陆系统中，请等候。",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      const res = await resLoginApiCheckLogin(params);
      if (res.code === IS_OK) {
        setTimeout(() => {
          loading.close();
          this.$router.push({ path: "/projectSelect" });
        }, 500);
      } else {
        loading.close();
      }
    },
  },
};
</script>

<style lang="sass" scoped>
.login-wrap
  .left-basemap-box
    position: absolute
    left: 10%
    top: 50%
    width: 800px
    height: 760px
    margin-top: -380px
    z-index: 44
    .left-basemap
      width: 100%
      height: 100%
    .left-basemap-text
      width: 100%
      height: 100%
      position: relative
      .maintitle
        position: absolute
        top: -450px
        font-size: 52px
        font-weight: bold
        text-align: center
        color: rgb( 21, 69, 82)
        left: 0px
        width: 100%
      .subtitle
        position: absolute
        top: -450px
        width: 100%
        font-size: 52px
        font-weight: bold
        text-align: center
        background-image: linear-gradient(to right, #0bc8fe, #feea85)
        background-clip: text
        color: transparent
        -webkit-background-clip: text
        left: 1px
  .login-form
    position: absolute
    right: 212px
    top: 50%
    width: 496px
    height: 490px
    margin-top: -245px
    background: url('../assets/img/login/login-form-bg.png')
    z-index: 44
    .login-form-warp
      position: relative
      width: 100%
      height: 100%
      .login-form-warp-body
        padding: 60px 100px 60px 70px
        .login-form-title
          margin: 25px 0 62px 30px
          font-size: 26px
          color: rgb( 0, 243, 255)
          font-weight: bold
          line-height: 1.333
          text-align: center
        .form-group
          border-bottom: 1px solid rgba( 255, 255, 255, 0.1)
          margin-bottom: 10px
          padding-bottom: 10px
          .form-group-label
            float: left
            font-size: 15px
            color: rgb( 0, 243, 255)
            line-height: 0.625
            text-align: left
            display: flex
            justify-content: center
            align-items: center
            height: 38px
            > img
              width: 23px
              height: 23px
              margin-right: 6px
          .form-group-control
            margin-left: 75px
            > input
              height: 38px
              line-height: 38px
              background-color: #00000000
              font-size: 14px
              color: #fff
              border: 0
              margin: 0px
              margin-left: 15px
              outline: none
              &::placeholder
                color: rgb( 255, 255, 255)
      .login-form-warp-footer
        position: absolute
        bottom: -3px
        left: 1px
        height: 72px
        width: 464px
        background-image: linear-gradient(to right, #00c8ec, #0092d6)
        border: 0
        margin: 17px
        display: flex
        justify-content: center
        align-items: center
        cursor: pointer
        overflow: hidden
        &::after
          content: ""
          position: absolute
          left: 0px
          bottom: 0px
          width: 0
          height: 0
          border-color: #0b3950 transparent
          border-width: 0 21px 21px 0
          border-style: solid
        &::before
          content: ""
          position: absolute
          right: 0px
          bottom: 0px
          width: 0
          height: 0
          border-color: #0d2034 transparent
          border-width: 0 0 21px 21px
          border-style: solid
        &:hover
          opacity: .9
          cursor: pointer
        button
          background: transparent
          border: none
          color: #fff
          font-size: 22px
          color: rgb( 255, 255, 255)
          line-height: 0.455
          text-align: center
          margin-left: 24px
          display: flex
          align-items: center
          cursor: pointer
          outline: none
          > img
            margin-right: 10px
</style>
