<template>
  <Header />
  <br />
  <h1>Hello {{ name }}, Welcome to Home page</h1>
  <span class="search-bar">
    <input type="text" placeholder="Enter Name to search" v-model="search" />
    <button title="Search a restaurant" @click="searchRestaurant">
      Search
    </button>
  </span>

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
      search: "",
      restaurant: [],
    };
  },
  methods: {
    searchRestaurant() {
      const restaurantName = this.search;
      const list = this.restaurant.filter((item) =>
        item.name.includes(this.search)
      );
      this.restaurant = list;
    },
    async loadData() {
      const user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "SignUp" });
        return;
      }
      this.name = JSON.parse(user).name;
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
.search-bar {
  width: min-content;
  height: min-content;
  position: absolute;
  right: 10px;
  top: 60px;
  gap: 20px;
  display: flex;
}
.search-bar input {
  /* height: 100%; */
  width: 160px;
  height: 40px;
  padding-left: 20px;
  display: block;
  border: 1px solid skyblue;
}
.search-bar button {
  width: 150px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
  cursor: pointer;
}
.search-bar button:hover {
  background-color: #f5f5f5;
  color: skyblue;
}
ul {
  width: 80%;
  margin-top: 10px;
  justify-content: center;
  display: flex;
  flex-wrap: wrap;
  list-style-type: none;
  border-radius: 50px;
  /* background-color: rgb(238, 237, 235); */
  /* border: 1px solid black; */
}
</style>
