<template>
    <div class="update">
        <h1>Update Cafe</h1>
		<input type="text" placeholder="Enter Name" v-model="model.name"/>
		<input type="text" placeholder="Enter Address" v-model="model.address"/>
		<input type="text" placeholder="Enter Contact" v-model="model.contact"/>
		<button @click="updateCafe" style="cursor:pointer">Update Cafe</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    name: 'UpdateCafeComponent',
    data() {
      return {
        model: {
          id: '',
          name: '',
          address: '',
          contact: ''
        }
      };
    },
    created() {
      const cafeId = this.$route.params.id;
      axios.get(`http://localhost:3000/cafe/${cafeId}`)
        .then(response => {
          this.model = response.data;
        })
        .catch(error => {
          console.log('ERROR', error);
        });
    },
    methods: {
      updateCafe() {
       const cafeId = this.model.id;
       axios.put(`http://localhost:3000/cafe/${cafeId}`, this.model)
        .then(response => {
          this.model = response.data;
          this.$router.push('/');
        })
        .catch(error => {
          console.log('ERROR', error);
        });
      }
    }
  };
</script>
<style scoped>
  .update input{
      border: 1px solid skyblue;
      width: 300px;
      height: 40px;
      margin-bottom: 15px;
      padding-left: 20px;
      display: block;
      margin-left: auto;
      margin-right: auto;
  }
  
  .update button{
      width: 320px;
      height: 40px;
      border: 1px solid skyblue;
      color: #fff;
      background-color: skyblue;
  }
  
  .update h1{
      text-align: center;
  
  }.update {
      text-align: center;
  }
  
  .update img{
      margin-bottom: 14px;
  }
</style>
  