<template>
  <div class="home">
    <h2>{{ post.title }}</h2>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <p>{{ post.body }}</p>
    <p>Added: {{ time(post.created_at) }}</p>
    <p>Last Edit: {{ time(post.updated_at) }}</p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit Post</router-link>
    |
    <a href="/">Home</a>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  border: 12px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;
}

img {
  width: 250px;
  height: 350px;
}

h2 {
  font-style: italic;
  border-top-style: dashed;
  border-bottom-style: dashed;
  border-left-style: solid;
  border-right-style: solid;
}

.home {
  margin: 0 auto;
  padding: 10px 25px;
  border: 3px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;

  background: rgb(228, 226, 226);

  text-align: center;
}
</style>

<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.postsShow();
  },
  methods: {
    postsShow: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.post = response.data;
        console.log(response.data);
      });
    },
    time: function (info) {
      return moment(info).format("MMMM Do YYYY, h:mm:ss a");
    },
  },
};
</script>
