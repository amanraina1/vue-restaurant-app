<template>
  <div class="image-container">
    <img :src="cloudinaryImageId" alt="restaurant image" />
    <div class="details">
      <h3 class="name">{{ name }}</h3>
      <span class="ratings">⭐️{{ avgRating }} • {{ contact }}</span>
      <span class="address">{{ address }}</span>
      <div class="icon">
        <router-link :to="'/update/' + id" v-if="isAdmin">
          <img title="Update" src="../assets/update.png" />
        </router-link>
        <router-link :to="'/review/' + id">
          <button title="See Reviews">See Reviews</button>
        </router-link>
        <img
          title="Delete"
          v-on:click="removeRestaurants(id)"
          v-if="isAdmin"
          src="../assets/delete.png"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  name: "Card",
  data() {
    return {
      isAdmin: "",
    };
  },
  props: {
    name: String,
    address: String,
    avgRating: String,
    contact: String,
    cloudinaryImageId: String,
    id: String,
  },
  methods: {
    ...mapActions(["removeRestaurants"]),
  },
  mounted() {
    const user = localStorage.getItem("user-info");
    this.isAdmin = JSON.parse(user).isAdmin;
  },
};
</script>

<style scoped>
.details .icon img {
  width: 30px;
  height: 30px;
}

.image-container {
  width: 273px;
  height: 340px;
  margin-right: 50px;
  margin-left: 50px;
  margin-top: 20px;
  margin-bottom: 20px;
  /* border: 1px solid black; */
  border-radius: 20px;
  overflow: hidden;
}
.image-container:hover {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  scale: 0.9;
  border-radius: 0px;
  transition: all 0.05s ease;
  border-bottom: 1px solid black;
  background-color: #f6f6f6;
}
.image-container img {
  width: 100%;
  /* height: 182px; */
  height: 65%;
  object-fit: cover;
  /* border-radius: 20px; */
}
.details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 35%;
}
.name {
  /* background-color: red; */
  width: 100%;
  height: 20%;
  /* width: 90%;
  display: block;
  font-size: 20px;
  margin: 5px;
  font-weight: 700; */
}

.ratings {
  /* background-color: yellow; */
  width: 100%;
  height: 15%;
  /* display: block;
  margin: 5px;
  width: 100%; */
}

.address {
  /* display: block; */
  /* background-color: lightblue; */
  height: 15%;
}

.icon {
  width: 100%;
  height: 40%;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  /* background-color: blue; */
}

.icon img {
  cursor: pointer;
  /* width: 100px; */
  /* background-color: green; */
}
button {
  padding: 5px 10px;
  border-radius: 5px;
  color: white;
  background-color: rgb(89, 145, 250);
  border: none;
  cursor: pointer;
  font-weight: 700;
}
</style>
