<template>
	<div class="register">
		<h1>Sign Up</h1>
		<img src='@/assets/restologo.png'/>
		<input type="text" placeholder="Enter Name" v-model="model.name" />
		<input type="text" placeholder="Enter Email" v-model="model.email" />
		<input type="text" placeholder="Enter Password" v-model="model.password" />
		<button @click="signUp" style="cursor:pointer">Sign Up</button>
		<p><router-link to="/login">Login</router-link></p>
	</div>
</template>


<script>
import axios from 'axios';

	export default{
		name: 'SignUp',
		data() {
			return{
				model: {
					name: '',
					email: '',
					password: '',
				}
			}
		},
		methods: {
			signUp(){
				if(!this.model.name || !this.model.email || !this.model.password){
					alert('please fill all the details')
					return;
				}
				axios.post('http://localhost:3000/user', this.model)
					.then(response => {
						if (response.status == 201){
							alert('signup complete')
							localStorage.setItem('user-info', JSON.stringify(response.data));
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
	}
</script>

<style scoped>
.register input{
    border: 1px solid skyblue;
    width: 300px;
    height: 40px;
    margin-bottom: 15px;
    padding-left: 20px;
    display: block;
    margin-left: auto;
    margin-right: auto;
}

.register button{
	width: 320px;
	height: 40px;
	border: 1px solid skyblue;
	color: #fff;
	background-color: skyblue;
}

.register h1{
	text-align: center;

}.register {
    text-align: center;
}

.register img{
	margin-bottom: 14px;
}
</style>