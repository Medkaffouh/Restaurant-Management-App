<template>
  <div class="container">
    <HeaderComponent />
    <h1>Hello {{name}}, Welcome on Home Page</h1>
  </div>
</template>
<script>
import HeaderComponent from "./Header.vue"
export default {
  name: 'HomeComponent',
  data(){
    return{
      name:''
    }
  },
  components:{
    HeaderComponent
  },
  mounted() {
    let user= localStorage.getItem('user-info');
    this.name= JSON.parse(user).name;
    if(!user){
      this.$router.push({name:'Login'})
    }
  }
};
</script>
<style scoped>

</style>
