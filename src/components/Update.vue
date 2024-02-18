<template>
  <Header />
  <br /><br />
  <h1>Hello User, Update a restaurant</h1>
  <br /><br />
  <form class="update">
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
      type="text"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
      name="contact"
    />
    <input
      type="text"
      placeholder="Enter Ratings"
      v-model="restaurant.avgRating"
      name="avgRating"
    />
    <input
      type="text"
      placeholder="Restaurant Image Link"
      v-model="restaurant.cloudinaryImageId"
      name="cloudinaryImageId"
    />
    <button type="button" v-on:click="updateRestaurant">
      Update Restaurant
    </button>
  </form>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
  data() {
    return {
      id: this.$route.params.id,
      restaurant: {
        name: "",
        address: "",
        contact: "",
        cloudinaryImageId: "",
        avgRating: "",
      },
    };
  },
  methods: {
    async updateRestaurant() {
      if (this.restaurant.avgRating === "") {
        this.restaurant.avgRating = "4";
      }
      if (this.restaurant.cloudinaryImageId === "") {
        this.restaurant.cloudinaryImageId =
          "../assets/placeholder-restaurant.png";
      }
      let result = await axios.put(
        `http://127.0.0.1:3000/restaurants/${this.id}`,
        {
          name: this.restaurant.name,
          contact: this.restaurant.contact,
          address: this.restaurant.address,
          cloudinaryImageId: this.restaurant.cloudinaryImageId,
          avgRating: this.restaurant.avgRating,
        }
      );
      if (result.status === 200) {
        this.$router.push({ name: "Home" });
      }
    },
  },
  components: {
    Header,
  },
  async mounted() {
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }

    let details = await axios.get(
      `http://localhost:3000/restaurants/${this.id}`
    );
    if (details) {
      this.restaurant.name = details.data.name;
      this.restaurant.address = details.data.address;
      this.restaurant.contact = details.data.contact;
      this.restaurant.cloudinaryImageId = details.data.cloudinaryImageId;
      this.restaurant.avgRating = details.data.avgRating;
    }
  },
};
</script>
