<template>
  <div>
    <h2>World New</h2>
    <div>{{ getposts }}</div>
    <div v-for="post in posts" :key="post.id">
      <h3>{{ post.id }} {{ post.title }}</h3>
      <p>{{ post.body }}</p>
      <router-link :to="{ name: 'CommentList', params: { id: post.id } }">
        <button>Read more</button>
      </router-link>
      <hr />
    </div>
    <h3 v-if="errormsg">{{ errormsg }}</h3>
  </div>
</template>

<script>
import axios from "axios";
export default {
  //name: "PostList",
  data() {
    return {
      posts: [],
      errormsg: "",
    };
  },

  computed: {
    getposts() {
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then((responce) => {
          //console.log(responce.data);
          this.posts = responce.data;
        })
        .catch((e) => {
          console.log(e);
          this.errormsg = "error retrieving data";
        });
    },
  },
};
</script>

<style>
h2 {
  background: black;
  color: white;
  margin: 0px;
  padding: 24px;
  font-size: 30px;
}
body {
  margin: 0px;
}

button {
  background-color: black;
  padding: 7px;
  text-decoration: none;
  color: #fff;
  border-color: black;
  border-radius: 4px;
}
</style>