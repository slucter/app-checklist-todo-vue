<template>
  <div>
    <div class="container">
      <form @submit.prevent="login" class="box">
        <h2>Login</h2>
        <input type="text" placeholder="Username" v-model="username">
        <input type="password" placeholder="Password" v-model="password">
        <button type="submit">Login</button>
        <h4 style="margin-top: 15px;">Register? go to <router-link to="register">Register Page</router-link></h4>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Login',
  data () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    login () {
      axios.post('http://18.141.178.15:8080/login', {
        username: this.username,
        password: this.password
      }).then((result) => {
        if (result.data.statusCode === 2110) {
          localStorage.setItem('token', result.data.data.token)
          this.$router.push('/')
        }
      }).catch((error) => {
        console.log('error' + error)
      })
    }
  },
  mounted () {
    if (localStorage.token) {
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
.container{
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: aliceblue;
}
.box{
  width: 30%;
  height: 35%;
  background-color: cornsilk;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.box input{
  margin: 12px 0;
  border: 2px solid #cacaac;
  width: 80%;
  height: 30px;
  padding: 0 10px;
}

.box button{
  width: 20%;
  height: 40px;
  border-radius: 10px;

}
</style>
