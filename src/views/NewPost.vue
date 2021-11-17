<template>
  <div class="newpost">
    <form v-on:submit.prevent="createPost()">
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
        <input type="string" v-model="newPostParams.body" />
        <p></p>

        <small v-if="newPostParams.body.length <= 200 && newPostParams.body.length > 0">
          {{ 200 - newPostParams.body.length }} body letters remaining
        </small>
        <small v-if="newPostParams.body.length > 200" class="text-danger">
          {{ 200 - newPostParams.body.length }} body letters remaining
        </small>
      </div>
      <p></p>
      <div>
        <label>Image URL:</label>
        <p></p>
        <input type="string" v-model="newPostParams.image" />
      </div>
      <p></p>
      <button v-on:click="createPost()">Create</button>
    </form>
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
    };
  },
  methods: {
    createPost: function () {
      axios.post("/posts", this.newPostParams).then((response) => {
        console.log(response.data);
        this.posts.push(response.data);
      });
      this.newPostParams.title = "";
      this.newPostParams.body = "";
      this.newPostParams.image = "";
      this.$router.push("/");
      location.reload();
    },
  },
};
</script>
