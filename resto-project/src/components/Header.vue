<template>
  <div class="container">
    <ul class="list">
      <li class="listItem">Home</li>
      <li class="listItem">Add Restaurant</li>
      <li class="listItem">Update Restaurant</li>
      <li class="listItem">Logout</li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "HeaderComponent",
};
</script>
<style scoped>
.container {
  height: 50px;
  background-color: black;
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
  cursor: pointer;
  padding: 5px 10px;
  border-radius: 5px;
}

.listItem:hover{
    background-color: rgb(38, 38, 38);
}
</style>
