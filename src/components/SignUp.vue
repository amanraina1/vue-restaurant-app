<template>
  <img class="logo" src="../assets/resto-logo.jpg" />
  <h1>Signup Page</h1>
  <br />
  <div class="signup">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="email" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="sendData">Sign Up</button>
    <br /><br />
    <p>
      <router-link to="/login"> <button>Go To Login Page</button> </router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async sendData() {
      const result = await axios.post("http://127.0.0.1:3000/users", {
        name: this.name,
        email: this.email,
        password: this.password,
      });
      if (result.status === 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    const user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
<style></style>
