<template>
  <div class="container">
    <h1>Hello User, Welcome on Home Page</h1>
  </div>
</template>
<script>
export default {
  name: 'HomeComponent',
  mounted() {
    let user= localStorage.getItem('user-info');
    if(!user){
      this.$router.push({name:'SignUp'})
    }
  }
};
</script>
<style>
</style>
