<template>
  <router-view />
</template>

<script>
export default {
  name: "App",
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
* {
  margin: 0;
  padding: 0;
  background-color: #f5f5f5;
}
.logo {
  width: 200px;
}
.signup input,
.login input,
.add input,
.update input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  display: block;
  border: 1px solid skyblue;
}
.signup button,
.login button,
.add button,
.update button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
  cursor: pointer;
}
.signup button:hover,
.login button:hover,
.add button:hover,
update button:hover {
  background-color: #f5f5f5;
  color: skyblue;
}
</style>
