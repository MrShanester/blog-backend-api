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

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
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
