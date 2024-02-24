<template>
  <Header />
  <br /><br />
  <div class="container">
    <h1>Hello {{ username }}, Review a restaurant</h1>
    <br /><br />
    <ul>
      <li v-for="item in reviews" :key="item">
        <div class="info">
          <span class="profile">
            <img src="../assets/avatar.svg" alt="user avatar" />
            <b>{{ item.name }} </b>
          </span>
          <span>{{ item.rating }}⭐️</span>
        </div>
        <h4>{{ item.message }}</h4>
      </li>
    </ul>
    <div class="comments">
      <input
        type="text"
        v-model="message"
        placeholder="Write a Review (optional)"
        name="review"
      />
      <label for="rating">Rating : </label>
      <select name="rating" id="rating" v-model="rating">
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
        <option value="4">4</option>
        <option value="5">5</option>
      </select>
      <br />
      <br />
      <br />
      <button @click="print">Submit</button>
    </div>
  </div>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Review",
  data() {
    return {
      rating: "",
      username: "",
      message: "",
      id: this.$route.params.id,
      reviews: [],
      restaurant: {
        name: "",
        conatct: "",
        address: "",
        cloudinaryImageId: "",
        avgRating: "",
      },
    };
  },
  methods: {
    async print() {
      const user = localStorage.getItem("user-info");
      const userId = JSON.parse(user).id;
      const name = JSON.parse(user).name;
      this.reviews = [
        ...this.reviews,
        {
          id: userId,
          name: name,
          message: this.message,
          rating: this.rating,
        },
      ];
      //   console.log(this.reviews);
      let result = await axios.put(
        `http://127.0.0.1:3000/restaurants/${this.id}`,
        {
          name: this.restaurant.name,
          contact: this.restaurant.contact,
          address: this.restaurant.address,
          cloudinaryImageId: this.restaurant.cloudinaryImageId,
          avgRating: this.restaurant.avgRating,
          reviews: this.reviews,
        }
      );
      console.log(result);
    },
  },
  components: {
    Header,
  },
  async mounted() {
    const user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
      return;
    }
    this.username = JSON.parse(user).name;
    let details = await axios.get(
      `http://localhost:3000/restaurants/${this.id}`
    );
    if (details) {
      this.restaurant.name = details.data.name;
      this.restaurant.address = details.data.address;
      this.restaurant.contact = details.data.contact;
      this.restaurant.cloudinaryImageId = details.data.cloudinaryImageId;
      this.restaurant.avgRating = details.data.avgRating;
      this.reviews = details.data.reviews;
    }
  },
};
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  width: 100vw;
  height: 100vh;
  overflow-y: scroll;
}
ul {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style: none;
  margin-bottom: 10px;
}
ul li {
  border: 2px solid rgb(162, 162, 162);
  margin: 20px;
  list-style: none;
  width: 30%;
  padding: 10px;
  gap: 20px;
  height: 80px;
  display: flex;
  flex-direction: column;
  /* background-color: red; */
}
ul li .info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}
ul li .info .profile {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}
ul li img {
  width: 30px;
}
ul li h4 {
  display: flex;
}
</style>
