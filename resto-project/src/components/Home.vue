<template>
  <div class="container">
    <HeaderComponent />
    <h1>Hello User, Welcome on Home Page</h1>
  </div>
</template>
<script>
import HeaderComponent from "./Header.vue"
export default {
  name: 'HomeComponent',
  components:{
    HeaderComponent
  },
  mounted() {
    let user= localStorage.getItem('user-info');
    if(!user){
      this.$router.push({name:'Login'})
    }
  }
};
</script>
<style scoped>

</style>
