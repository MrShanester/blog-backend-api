<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-info">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navigation</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="/">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/newpost">Create a Post</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Account
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <div v-if="isLoggedIn()">
                  <li><a class="dropdown-item" href="/login">Log-in</a></li>
                  <li><a class="dropdown-item" href="/signup">Sign-Up</a></li>
                </div>
                <div v-if="isLoggedIn() == false">
                  <li><a class="dropdown-item" href="/logout">Sign Out</a></li>
                </div>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div v-if="flashMessage" class="alert alert-success">
      {{ flashMessage }}
      <button class="but" v-on:click="reload()">x</button>
    </div>

    <router-view />
  </div>
</template>

<style>
.but {
  text-align: right;
}

h1 {
  text-align: center;
}

h2 {
  text-align: center;
}

p {
  text-align: center;
}

body {
  background-image: url(./assets/grey_wash_wall.png);
  text-align: center;
}
</style>

<script>
// import axios from "axios";

export default {
  data: function () {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return false;
      } else {
        return true;
      }
    },
    reload: function () {
      location.reload();
    },
  },
};
</script>
