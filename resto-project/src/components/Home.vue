<template>
  <div class="container">
    <HeaderComponent />
    <h1>Hello {{ name }}, Welcome on Home Page</h1>
    <table border="1">
      <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Contact</td>
        <td>Address</td>
        <td>Actions</td>
      </tr>
      <tr v-for="item in restaurants" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.contact }}</td>
        <td>{{ item.address }}</td>
        <td>
          <router-link :to="'/update/' + item.id">Update</router-link> -
          <button v-on:click="deleteRestaurant(item.id)">Delete</button>
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
import HeaderComponent from "./Header.vue";
import axios from "axios";
export default {
  name: "HomeComponent",
  data() {
    return {
      name: "",
      restaurants: [],
    };
  },
  components: {
    HeaderComponent,
  },
  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      console.warn(result);
      if (result.status == 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "Login" });
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      console.warn(result);
      this.restaurants = result.data;
    },
  },
  async mounted() {
    this.loadData();
  },
};
</script>
<style scoped>
.container {
  text-align: center;
}
td {
  width: 140px;
  height: 40px;
  text-align: center;
}
</style>
