<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'home' }">Home</router-link>
    <router-link :to="{ name: 'AddProject' }">Add Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  margin: 20px 0;
  text-align: center;
}
.main-nav a {
  text-decoration: none;
  color: #888;
  margin: 0 10px;
  letter-spacing: 1px;
  font-weight: bold;
  box-sizing: border-box;
  text-transform: uppercase;
  border-bottom: 2px solid transparent;
  transition: border-bottom-color 0.5s ease-in-out;
}
.main-nav a.router-link-exact-active {
  border-bottom-color: rgb(18, 186, 18);
}
</style>
