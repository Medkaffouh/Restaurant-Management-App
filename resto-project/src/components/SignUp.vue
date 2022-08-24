<template>
  <div class="container">
    <h1 class="logo">RESTO</h1>
    <h1>Sign Up</h1>
    <div class="register">
      <input type="text" v-model="name" placeholder="Enter Name" />
      <input type="text" v-model="email" placeholder="Enter Email" />
      <input type="password" v-model="password" placeholder="Enter Password" />
      <button v-on:click="signUp()" class="button">Sign Up</button>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUpComponent",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      let result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        password: this.password,
        name: this.name,
      });

      console.warn(result);
      if(result.status==201){
        localStorage.setItem("user-info",JSON.stringify(result.data));
        this.$router.push({name:'Home'})
      }
    },
  },
  mounted() {
    let user= localStorage.getItem('user-info');
    if(user){
      this.$router.push({name:'Home'})
    }
  }
};
</script>

<style>
.container{
    text-align: center;
  margin-top: 60px;
}
.logo {
  font-weight: 700;
  font-size: 70px;
  color: teal;
}

.register input {
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
