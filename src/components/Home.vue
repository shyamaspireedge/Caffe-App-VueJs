<template>
	<HeaderLink />
	<h1 class="text">{{ userName }}, Welcome to Home Page..!!!</h1>
	<div v-if="cafes.length > 0">
		<table class="custom-table">
			<tr>
				<td>Name</td>
				<td>Address</td>
				<td>Contact</td>
				<td>Action</td>
			</tr>
			<tr v-for="item in cafes" :key="item.id">
				<td>{{ item.name }}</td>
				<td>{{ item.address }}</td>
				<td>{{ item.contact }}</td>
				<td class="actions-column">
					<router-link :to="'/update/' + item.id" class="action-link">Update</router-link>
					|
					<button @click="deleteCafe(item.id)" style="cursor: pointer;">Delete</button>
				</td>
			</tr>
		</table>
	</div>
	<div v-else>
		<p>No records found.</p>
	</div>
</template>

<script>
import HeaderLink from './HeaderLink.vue'
import axios from 'axios';

export default{
	name: 'HomePage',
	components: {
		HeaderLink
	},
	data() {
		return{
			userName:'',
			cafes: [],
		}
	},
	methods: {
		deleteCafe(id) {
			axios.delete(`http://localhost:3000/cafe/${id}`)
				.then(response => {
					if (response.status === 200) {
						this.cafes = this.cafes.filter(cafe => cafe.id !== id);
					}
				})
				.catch(error => {
					console.error('Error deleting cafe:', error);
				});
		}
	},
	async mounted() {
		let user = localStorage.getItem('user-info');
		if(user){
			let name = JSON.parse(user).name;
			this.userName = name				
		}
		else{
			this.$router.push('/sign-up')
		}

		axios.get('http://localhost:3000/cafe')
			.then(response => this.cafes = response.data)
			.catch(error => {console.log('ERROR', error)})
	}
}
</script>

<style scoped>
.custom-table {
	width: 100%;
    max-width: 30%;
    margin: 0 auto;
    border-collapse: collapse;
	margin-top: 100px;
}
.custom-table th, .custom-table td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: left;
}

.actions-column {
  text-align: center;
}

.action-link {
  text-decoration: none;
  margin-right: 10px;
  color: blue;
}

.action-link:hover {
  text-decoration: underline;
}

.no-records {
  text-align: center;
  margin-top: 20px;
}
.text{
	text-align: center;
}
</style>
