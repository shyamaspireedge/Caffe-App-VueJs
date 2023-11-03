<template>
  <div class="register">
    <h1>Login</h1>
    <img src="@/assets/restologo.png" />
    <input type="text" placeholder="Enter Email" v-model="model.email" />
    <input type="text" placeholder="Enter Password" v-model="model.password" />
    <button @click="loginBtn" class="login-btn">Login</button>
    <p><router-link to="/sign-up">Sign up</router-link></p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LogIn',
  data() {
    return {
      model: {
        email: '',
        password: '',
      },
    };
  },
  methods: {
    async loginBtn() {
      if (!this.model.email || !this.model.password) {
        alert('Please fill all the details');
        return;
      }
      await axios.get(`http://localhost:3000/user?email=${this.model.email}&password=${this.model.password}`)  
                .then(response => {
                  if (response.status == 200){
                    alert('login complete')
                    localStorage.setItem('user-info', JSON.stringify(response.data[0]));
                    this.$router.push('/');
                  }
                })
                .catch(error => {console.log('error:', error)})
    },
  },
  mounted() {
    let user = localStorage.getItem('user-info');
    if (user){
      this.$router.push('/')
    }
  }
};
</script>

<style scoped>
.register input {
  border: 1px solid skyblue;
  width: 300px;
  height: 40px;
  margin-bottom: 15px;
  padding-left: 20px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}

.register button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
}

.register h1 {
  text-align: center;
}

.register {
  text-align: center;
}

.register img {
  margin-bottom: 14px;
}

.login-btn {
  cursor: pointer;
}
</style>
