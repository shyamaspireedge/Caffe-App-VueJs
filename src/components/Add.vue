<template>
    <HeaderLink />
    <div class="register">
        <h1>Add Cafe</h1>
		<input type="text" placeholder="Enter Name" v-model="model.name"/>
		<input type="text" placeholder="Enter Address" v-model="model.address"/>
		<input type="text" placeholder="Enter Contact" v-model="model.contact"/>
		<button @click="addCafe" style="cursor:pointer">Add New Cafe</button>
	</div>
</template>

<script>
import HeaderLink from './HeaderLink.vue'
import axios from 'axios'

    export default {
       name: 'AddCafe',
       components: {
            HeaderLink
       },
       data() {
        return{
            model:{
                name: '',
                address: '',
                contact:'',
            }
        }
       },
       methods: {
        addCafe() {
            axios.post('http://localhost:3000/cafe', this.model)
                .then(response => {
                    if (response.status == 201){
                        // console.log(response.data)
                        this.$router.push('/');
                    }
                })
                .catch(error => {console.log("Error", error)})
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