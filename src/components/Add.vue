<template>
  <Header />
  <br />
  <div class="breadcrumbs-path">
    <router-link to="/">Home </router-link>
    <div v-for="(path, index) in fullPaths">
      <span v-if="index === fullPaths.length - 1"> / {{ path }}</span>
      <span v-else
        >/<router-link to="path">{{ path }} </router-link></span
      >
    </div>
  </div>
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
      placeholder="Image Link (if no link, default will be added)"
      v-model="restaurant.cloudinaryImageId"
      name="image"
    />
    <button type="button" v-on:click="addRestaurantNew">Add Restaurant</button>
  </form>
</template>
<script>
import Header from "./Header.vue";
import { mapActions } from "vuex";
export default {
  name: "Add",
  data() {
    return {
      username: "",
      fullPaths: "",
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
    ...mapActions(["addRestaurants"]),
    async addRestaurantNew() {
      if (this.restaurant.avgRating === "") {
        this.restaurant.avgRating = "4";
      }
      if (this.restaurant.cloudinaryImageId === "") {
        this.restaurant.cloudinaryImageId =
          "/src/assets/placeholder-restaurant.png";
      }
      this.addRestaurants({
        restaurantName: this.restaurant.name,
        contact: this.restaurant.contact,
        address: this.restaurant.address,
        cloudinaryImageId: this.restaurant.cloudinaryImageId,
        avgRating: this.restaurant.avgRating,
        reviews: [],
      });

      this.$router.push({ name: "Home" });
    },
  },
  mounted() {
    let user = localStorage.getItem("user-info");
    const { fullPath } = this.$route;
    this.fullPaths = fullPath.split("/").filter((x) => x);
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
