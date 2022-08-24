<template>
  <div class="container">
    <h1 class="logo">RESTO</h1>
    <h1>Login</h1>
    <div class="login">
      <input type="text" v-model="email" placeholder="Enter Email" />
      <input type="password" v-model="password" placeholder="Enter Password" />
      <button v-on:click="login" class="button">Login</button>
      <p>
        <router-link to="/sign-up">Sign Up</router-link>
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "LoginComponent",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      console.log(result);
      if (result.status == 200 && result.data.length>0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted(){
    let result = localStorage.getItem("user-info");
    if(result){
        this.$router.push({name:"Home"});
    }
  }
};
</script>
<style scoped>
.container {
  text-align: center;
  margin-top: 60px;
}
.logo {
  font-weight: 700;
  font-size: 70px;
  color: teal;
}

.login input {
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
