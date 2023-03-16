<template>
  <div>
    <!-- <h2>World New</h2> -->
    <!-- <div>{{ getcomments }}</div> -->
    <div v-for="comment in comments" :key="comment.id">
      <h3>{{ comment.id }} {{ comment.name }}</h3>
      <h4>{{ comment.email }}</h4>
      <p>{{ comment.body }}</p>
      <hr />
    </div>
    <h3 v-if="errormsg" class="err">{{ errormsg }}</h3>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";
export default {
  //name: "CommentList",
  props: ["id"],

  setup(props) {
    const comments = ref([]);
    let errormsg = ref("");

    axios
      .get("https://jsonplaceholder.typicode.com/comments?postId=" + props.id)
      .then((responce) => {
        console.log(responce.data);
        comments.value = responce.data;
      })
      .catch((e) => {
        console.log(e);
        errormsg.value = "error retrieving data";
      });

    return { comments, errormsg };
  },

  // data() {
  //   return {
  //     comments: [],
  //     errormsg: "",
  //   };
  // },

  // computed: {
  //   getcomments(props) {
  //     axios
  //       .get("https://jsonplaceholder.typicode.com/comments?postId=" + props.id)
  //       .then((responce) => {
  //         console.log(responce.data);
  //         this.comments = responce.data;
  //       })
  //       .catch((e) => {
  //         console.log(e);
  //         this.errormsg = "Error Retrieving Data";
  //       });
  //   },
  // },
};
</script>

<style>
.err {
  color: red;
}
</style>