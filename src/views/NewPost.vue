<template>
  <div class="newpost">
    <form v-on:submit.prevent="">
      <h1>Make a Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <p></p>
        <input type="string" v-model="newPostParams.title" />
      </div>
      <p></p>
      <div>
        <label>Body:</label>
        <p></p>
        <input type="string" v-model="newPostParams.body" maxlength="100" />
        <p></p>
        <small v-if="newPostParams.body.length == 0"></small>
        <small v-else-if="newPostParams.body.length < 100 && newPostParams.body.length > 0">
          {{ 100 - newPostParams.body.length }} body letters remaining
        </small>
        <small v-else class="text-danger">0 body letters remaining</small>
      </div>
      <p></p>
      <div>
        <label>Image URL:</label>
        <p></p>
        <input type="string" v-model="newPostParams.image" />
      </div>
      <p></p>
      <button v-on:click="createPost()">Create</button>
      <p></p>
    </form>
    <p v-if="status == 401">Try Signing In</p>
    <p></p>
    <img v-if="status" :src="`https://http.cat/${status}`" />
  </div>
</template>

<style scoped>
.newpost {
  text-align: center;
}
</style>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { body: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log(response.data);
          this.posts.push(response.data);
        })
        .catch((error) => {
          this.status = error.response.status;

          console.log(error.response.data);
        });
      // this.newPostParams.title = "";
      // this.newPostParams.body = "";
      // this.newPostParams.image = "";
      // this.$router.push("/");
      // location.reload();
    },
  },
};
</script>
