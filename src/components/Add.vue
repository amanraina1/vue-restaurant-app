<template>
  <Header />
  <br /><br />

  <h1>Hello User, Add a new restaurant</h1>
  <br /><br />

  <form class="add">
    <input
      type="text"
      placeholder="Enter Name"
      v-model="restaurant.name"
      name="name"
    />
    <input
      type="text"
      placeholder="Enter Address"
      v-model="restaurant.address"
      name="address"
    />
    <input
      type="number"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
      name="contact"
    />
    <input
      type="text"
      placeholder="Image Link"
      v-model="restaurant.imageLink"
      name="image"
    />
    <button type="button" v-on:click="addRestaurant">Add Restaurant</button>
  </form>
</template>
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  nmae: "Add",
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
        imageLink: "",
      },
    };
  },
  components: {
    Header,
  },
  methods: {
    async addRestaurant() {
      let result = await axios.post("http://localhost:3000/restaurants", {
        name: this.restaurant.name,
        contact: this.restaurant.contact,
        address: this.restaurant.address,
      });
      if (result.status === 201) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
