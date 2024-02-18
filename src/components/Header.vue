<template>
  <div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="add">Add Restaurant</router-link>
    <a v-on:click="logout">Logout</a>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "Login" });
    },
  },
};
</script>
<style>
.nav {
  background-color: skyblue;
  overflow: hidden;
  display: flex;
  justify-content: space-between;
}

.nav a {
  cursor: pointer;
  background-color: skyblue;
  float: left;
  color: #f5f5f5;
  font-weight: 700;
  text-align: center;
  padding: 10px 14px;
  text-decoration: none;
  font-size: 20px;
  margin-left: 40px;
  margin-right: 40px;
}
.nav a:hover {
  background-color: #f5f5f5;
  color: skyblue;
  transition: all 0.5s ease-in-out;
}
</style>
