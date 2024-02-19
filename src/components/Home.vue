<template>
  <Header />
  <br />
  <h1>Hello {{ name }}, Welcome to Home page</h1>

  <ul>
    <!-- <img src="../assets/placeholder-restaurant.png" /> -->
    <li v-for="item in restaurant" :key="item.id">
      <Card
        :name="item.name"
        :address="item.address"
        :avgRating="item.avgRating"
        :contact="item.contact"
        :cloudinaryImageId="item.cloudinaryImageId"
        :id="item.id"
      />
    </li>
  </ul>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
import Card from "./Card.vue";
export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  methods: {
    async loadData() {
      const user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get("http://localhost:3000/restaurants");
      this.restaurant = result.data;
    },
  },
  components: {
    Header,
    Card,
  },
  mounted() {
    this.loadData();
  },
};
</script>
<style scoped>
body {
  display: flex;
  justify-content: center;
  align-items: center;
}
ul {
  margin-top: 10px;
  justify-content: space-between;
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  /* border: 1px solid black; */
}
</style>
