<template>
  <div class="container">
    <HeaderComponent />
    <h1>Hello User, Welcome on Update Page</h1>
    <form class="update">
      <input type="text" name="name" v-model="restaurant.name" placeholder="Enter Name" />
      <input type="text" name="address" v-model="restaurant.address" placeholder="Enter Address" />
      <input type="text" name="contact" v-model="restaurant.contact" placeholder="Enter Contact" />
      <button v-on:click="updateRestaurant" type="button" class="button">Update Restaurant</button>
    </form>
  </div>
</template>
<script>
import HeaderComponent from "./Header.vue";
import axios from "axios";
export default {
  name: 'UpdateComponent',
  components:{
    HeaderComponent
  },
  data(){
    return{
      restaurant :{
        name:'',
        address:'',
        contact:''
      }
    }
  },
  methods:{
    async updateRestaurant(){
      let result = await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,{
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact
      });
      if(result.status==200){
        this.$router.push({name:"Home"})
      }
        console.log(result);
    }
  },
  async mounted() {
    let user= localStorage.getItem('user-info');
    if(!user){
      this.$router.push({name:'Login'})
    }
    const result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id);
    //console.warn(this.$route.params.id)
    console.warn(result)
    this.restaurant=result.data
  }
};
</script>
<style scoped>
.container{
  text-align: center;
}
.title{
    padding-bottom: 10px;
}
  .update input {
  width: 300px;
  height: 30px;
  display: flex;
  margin: 0 auto;
  margin-bottom: 20px;
  padding: 10px;
  font-weight: bold;
  font-size: 18px;
  border: 1px solid teal;
  border-radius: 5px;
  color: rgb(56, 56, 56);
}

.button {
  width: 320px;
  height: 40px;
  padding: 10px 20px;
  background-color: teal;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: 600;
  font-size: 16px;
}
.button:hover {
  background-color: rgb(35, 166, 166);
}
</style>
