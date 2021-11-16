<template>
  <div class="newpost">
    <form v-on:submit.prevent="updatePost()">
      <h1>Update Your Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <p></p>
        <input type="string" v-model="currentPostParams.title" />
      </div>
      <p></p>
      <div>
        <label>Body:</label>
        <p></p>
        <input type="string" v-model="currentPostParams.body" />
      </div>
      <p></p>
      <div>
        <label>Image URL:</label>
        <p></p>
        <input type="string" v-model="currentPostParams.image" />
      </div>
      <p></p>
      <button v-on:click="updatePost()">Update</button>
      |
      <a href="/">Back</a>
      |
      <button v-on:click="deletePost()">Delete</button>
    </form>
  </div>
</template>

<style scoped>
h1 {
  font-style: italic;
  border-top-style: dashed;
  border-bottom-style: dashed;
  border-left-style: solid;
  border-right-style: solid;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    this.postLoad();
  },
  methods: {
    updatePost: function () {
      axios.patch("/posts/" + this.$route.params.id, this.currentPostParams).then((response) => {
        console.log(response.data);
        this.$router.push("/");
      });
      this.newPostParams.title = "";
      this.newPostParams.body = "";
      this.newPostParams.image = "";
      this.$router.push("/");
      location.reload();
    },
    postLoad: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.currentPostParams = response.data;
      });
    },
    deletePost: function () {
      axios.delete("/posts/" + this.$route.params.id).then((response) => {
        console.log("Post destroyed", response.data);
        this.$router.push("/");
      });
    },
  },
};
</script>
