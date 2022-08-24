<template>
  <div class="container">
    <ul class="list">
      <li class="listItem">Home</li>
      <li class="listItem">Add Restaurant</li>
      <li class="listItem">Update Restaurant</li>
      <li v-on:click="logout" class="listItem">Logout</li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "HeaderComponent",
  methods:{
    logout(){
        localStorage.clear();
        this.$router.push({name:'Login'})
    }
  }
};
</script>
<style scoped>
.container {
  height: 50px;
  background-color: teal;
  color: white;
  display: flex;
  align-items: center;
  padding: 0 100px;
  font-size: 18px;
  justify-content: space-between;
  position: relative;
}

.listItem {
  display: inline;
  margin-right: 30px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  padding: 5px 10px;
  border-radius: 5px;
}

.listItem:hover{
    background-color: rgb(8, 187, 187);
}
</style>
