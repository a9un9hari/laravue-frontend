
<template>
  <div id="app">
    <form method="post" @submit.prevent="login"> 
      <input type="email" v-model="email">
      <input type="password" v-model="password">
      <button type="submit">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import Cookies from 'js-cookie'

export default {
  name: 'Login.vue',

  data: () => ({
    email : '',
    password : ''
  }),

  mounted() {

  },

  methods:{
    async login() {
      const { data } = await axios.post('http://laravue.test/api/login', {
        email : this.email,
        password : this.password
      })

      const apiToken = data.api_token;

      Cookies.set('token', apiToken);

      this.$router.push('/')
    }
  }

}
</script>