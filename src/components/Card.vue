<template>
  <div class="image-container">
    <img :src="cloudinaryImageId" alt="restaurant image" />
    <div class="details">
      <span class="name">{{ name }}</span>
      <span class="ratings">⭐️{{ avgRating }} • {{ contact }}</span>
      <span class="address">{{ address }}</span>
      <span class="icon">
        <router-link :to="'/update/' + id">
          <img src="../assets/update.png" />
        </router-link>
        <img v-on:click="deleteCard(id)" src="../assets/delete.png" />
      </span>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Card",
  props: {
    name: String,
    address: String,
    avgRating: String,
    contact: String,
    cloudinaryImageId: String,
    id: String,
  },
  methods: {
    async deleteCard(id) {
      let result = await axios.delete(
        `http://localhost:3000/restaurants/${id}`
      );
      if (result.status === 200) {
        alert("User deleted successfully");
      }
    },
    async updateCard(id) {
      console.log(id);
    },
  },
};
</script>
<style>
.details .icon img {
  width: 30px;
  height: 30px;
}

.image-container {
  width: 250px;
  height: 400px;
  margin: 50px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.image-container img {
  width: 100%;
  height: 65%;
  object-fit: cover;
}
.name {
  display: block;
  font-size: 20px;
  margin: 5px;
  font-weight: 700;
}
.ratings {
  display: block;
  margin: 5px;
  width: 100%;
}
.address {
  display: block;
}
.icon {
  width: 90%;
  display: flex;
  justify-content: space-between;
  padding: 10px;
}
.icon img {
  cursor: pointer;
}
</style>
