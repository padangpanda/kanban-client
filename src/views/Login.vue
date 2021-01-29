<template>
  <div class="container">
    <div class="row" style="display: flex; height: 100vh; align-items: center;">
      <div class="col-md-4 col-sm-4 col-xs-12"></div>
      <div class="col-md-4 col-sm-4 col-xs-12 rounded shadow-lg">
        <input type="radio" name="tab" id="tab-login" value="login" v-model="tab" checked> <label for="tab-login"><h4>Login</h4></label>
        <input type="radio" name="tab" id="tab-register" value="register" v-model="tab"> <label for="tab-register"><h4>Register</h4></label>
        <!-- Register -->
        <div id="register" v-if="tab === 'register'">   
          <form @submit.prevent="register">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input type="email" class="form-control" v-model="regemail" placeholder="Enter your email address">
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input type="password" class="form-control" v-model="regpassword" placeholder="Enter your password">
            </div>
            <button type="submit" class="btn btn-primary" id="register-btn" style="float: right;">Register</button>
          </form>
        </div>
        <!-- Login -->
        <div id="login" v-else>         
          <form @submit.prevent="login">
            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input type="email" class="form-control" v-model="email" placeholder="Enter your email address">
            </div>
            <div class="mb-3">
              <label for="password" class="form-label">Password</label>
              <input type="password" class="form-control" v-model="password" placeholder="Enter your password">
            </div>
            <button type="submit" class="btn btn-primary" id="login-btn" style="float: right;">Login</button>
            <button v-google-signin-button="clientId" class="google-signin-button"> Continue with Google</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import GoogleSignInButton from 'vue-google-signin-button-directive'

export default {
  props: ["baseUrl"],
  name: "Login",
  directives: {
    GoogleSignInButton
  },
  data() {
    return {
      regemail: '',
      regpassword: '',
      email: '',
      password: '',
      tab: '',
      clientId: '8648248464-jave4ho7n62vhri82s3pdpjo5b12j98e.apps.googleusercontent.com'
    }
  },
  methods: {
    login() {
      axios({
        method: 'POST',
        url: `${this.baseUrl}/login`,
        data: {
          email: this.email,
          password: this.password
        }
      })
      .then(({data}) => {
        console.log(data, '<<<<<<<<');
        localStorage.setItem('access_token', data.access_token)
        this.$emit('checkAuth')
      })
      .catch(err => console.log(err))
    },
    register() {
      axios({
        method: 'POST',
        url: `${this.baseUrl}/register`,
        data: {
          email: this.regemail,
          password: this.regpassword
        }
      })
      .then(({data}) => {
        console.log(data, 'hasil register');
        this.tab = 'login'
      })
      .catch(err => console.log(err))
    },
    OnGoogleAuthSuccess (idToken) {
      axios({
        method: 'POST',
        url: `${this.baseUrl}/loginGoogle`,
        data: {id_token}
      })
      .then(({data}) => {
        localStorage.setItem('access_token', data.access_token)
        this.$emit('checkAuth')
      })
      .catch(err => console.log(err))
    },
    OnGoogleAuthFail (error) {
      console.log(error)
    }
  }
}
</script>

<style scoped>
  .google-signin-button {
  color: white;
  background-color: red;
  height: 50px;
  font-size: 16px;
  border-radius: 10px;
  padding: 10px 20px 25px 20px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  }
</style>