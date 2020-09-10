<template>
  <div>
    <div class="container">
      <form @submit.prevent="register" class="box">
        <h2>Register</h2>
        <input type="text" placeholder="Email" v-model="email">
        <input type="text" placeholder="Username" v-model="username">
        <input type="password" placeholder="Password" v-model="password">
        <button type="submit">Register</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Register',
  data () {
    return {
      email: '',
      username: '',
      password: ''
    }
  },
  methods: {
    register () {
      axios.post('http://18.141.178.15:8080/register', {
        email: this.email,
        username: this.username,
        password: this.password
      }).then((result) => {
        if (result.data.statusCode === 2000) {
          alert('Berhasil Daftar, Silahkan Login')
          this.$router.push('/login')
        }
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
