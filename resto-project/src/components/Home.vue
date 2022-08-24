<template>
  <div class="container">
    <HeaderComponent />
    <h1>Hello {{name}}, Welcome on Home Page</h1>
    <table border="1">
      <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Contact</td>
        <td>Address</td>
      </tr>
      <tr v-for="item in restaurants" :key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.contact}}</td>
        <td>{{item.address}}</td>
      </tr>
    </table>
  </div>
</template>
<script>
import HeaderComponent from "./Header.vue";
import axios from "axios";
export default {
  name: 'HomeComponent',
  data(){
    return{
      name:'',
      restaurants: []
    }
  },
  components:{
    HeaderComponent
  },
  async mounted() {
    let user= localStorage.getItem('user-info');
    this.name= JSON.parse(user).name;
    if(!user){
      this.$router.push({name:'Login'})
    }
    let result = await axios.get("http://localhost:3000/restaurant");
    console.warn(result)
    this.restaurants=result.data;
  }
};
</script>
<style scoped>
  td{
    width: 140px;
    height: 40px;
    text-align: center;
  }
</style>
