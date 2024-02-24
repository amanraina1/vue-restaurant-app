<template>
  <img class="logo" src="../assets/resto-logo.jpg" />
  <h1>Login Page</h1>
  <br />
  <div class="login">
    <input type="email" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="login">LogIn</button>
    <br /><br />
    <p>
      <router-link to="/signup">
        <button>Go To Sign Up Page</button>
      </router-link>
    </p>
  </div>
  <br />
  <br />
  <br />
  <h4>For Admin Login</h4>
  <span>Email - admin@example.com | PW - admin</span>
  <br />
  <br />
  <h4>For User Login</h4>
  <span>Email - user@example.com | PW - user</span>
</template>
<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      {
        this.$router.push({ name: "Home" });
      }
    }
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      // if (result.data[0].isAdmin === true) {
      //   localStorage.setItem("user-info", JSON.stringify(result.data[0]));
      //   this.$router.push({ name: "Home" });
      // }
      if (result.status === 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
};
</script>
