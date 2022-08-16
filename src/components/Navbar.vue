<template>
  <div class="navbar">
    <router-link class="logo" to="/list">Список дел</router-link>
    <div class="link">
      <router-link class="linc" to="/">Добавить</router-link>
      <router-link class="linc" to="/list">Список</router-link>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
  background-color: teal;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.logo {
  font-size: 30px;
  text-decoration: none;
  color: white;
  padding: 5px;
}
.link {
  margin-right: 30px;
}
.linc {
  padding: 15px;
  font-size: 20px;
  text-decoration: none;
  color: white;
}
.logo:hover {
  background-color: #20b2aa;
}
.linc:hover {
  color: white;
  background-color: #20b2aa;
}
</style>
