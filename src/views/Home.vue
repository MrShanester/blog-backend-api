<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <div class="hyphen">
        <h2>{{ post.title }}</h2>
      </div>
      <div class="col d-flex justify-content-center">
        <div class="card" style="width: 18rem">
          <img v-bind:src="post.image" v-bind:alt="post.title" />
          <div class="selected">
            <div class="card-body">
              <p class="card-text">
                {{ post.body }}
              </p>
            </div>
          </div>
          <div class="selected2">
            <div class="col d-flex justify-content-center">
              <div class="card-body" id="button">
                <router-link v-bind:to="`/posts/${post.id}`">
                  <button>View Post</button>
                </router-link>
              </div>
            </div>
          </div>
        </div>
      </div>

      <p>---------------------------------</p>
    </div>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  border: 8px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;
}

p {
  text-align: center;
}

#button {
  text-align: center;
}

h2 {
  text-align: center;
  font-style: italic;
  border-top-style: dashed;
  border-bottom-style: dashed;
  border-left-style: solid;
  border-right-style: solid;
}

.hyphen:hover {
  text-align: center;
  height: 50px;
  border: 3px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;
}

.selected {
  background-color: aquamarine;
}

.selected2:hover {
  background-color: purple;
}

.home {
  margin: 0 auto;
  padding: 10px 25px;
  border: 3px solid;
  border-image: linear-gradient(135deg, #ff0000 0%, #49ff33 25%, #3364ff 50%, #f6ff33 75%, #ff00a8 100%) 1;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome To My Blog",
      posts: [],
      isActive: false,
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        this.posts = response.data;
      });
    },
    changeActive: function () {
      this.isActive = true;
    },
  },
};
</script>
