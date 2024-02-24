<template>
  <Header />
  <br /><br />

  <h1>Hello {{ username }}, Add a new restaurant</h1>
  <br /><br />

  <form class="add">
    <input
      type="text"
      placeholder="Enter Restaurant Name"
      v-model="restaurant.name"
      name="name"
    />
    <input
      type="text"
      placeholder="Enter Restaurant Address"
      v-model="restaurant.address"
      name="address"
    />
    <input
      type="text"
      placeholder="Enter Contact Number"
      v-model="restaurant.contact"
      name="contact"
    />
    <input
      type="text"
      placeholder="Image Link (if no image, default will be displayed)"
      v-model="restaurant.cloudinaryImageId"
      name="image"
    />
    <button type="button" v-on:click="addRestaurant">Add Restaurant</button>
  </form>
</template>
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  name: "Add",
  data() {
    return {
      username: "",
      restaurant: {
        name: "",
        address: "",
        contact: "",
        cloudinaryImageId: "",
        avgRating: "",
      },
    };
  },
  components: {
    Header,
  },
  methods: {
    async addRestaurant() {
      if (this.restaurant.avgRating === "") {
        this.restaurant.avgRating = "4";
      }
      if (this.restaurant.cloudinaryImageId === "") {
        this.restaurant.cloudinaryImageId =
          "/src/assets/placeholder-restaurant.png";
      }
      let result = await axios.post("http://localhost:3000/restaurants", {
        name: this.restaurant.name,
        contact: this.restaurant.contact,
        address: this.restaurant.address,
        cloudinaryImageId: this.restaurant.cloudinaryImageId,
        avgRating: this.restaurant.avgRating,
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
      return;
    }
    let admin = JSON.parse(user).isAdmin;
    if (user && !admin) {
      this.$router.push({ name: "Home" });
      return;
    }
    this.username = JSON.parse(user).name;
  },
};
</script>
