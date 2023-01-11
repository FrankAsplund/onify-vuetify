<template>

<!-- <div class="grid">
      <div v-for="post in posts" :key="post.id" class="for-class">
        <div class="user-container">
          <h1 class="user-h1">{{ post.id }}</h1>
          <h3 class="user-h3">{{ post.firstname }} {{ post.lastname }}</h3>
          <div class="user-text">Titel: {{ post.title }}</div>
          <div class="user-text">Telefonnummer: {{ post.phonenr }}</div>
          <div class="user-text">Bolag: {{ post.company }}</div>
          <div class="user-text">Avdelning: {{ post.department }}</div>
          <div class="user-text">Behörighet: {{ post.system }}</div>
          <button class="user-button" @click="deleteData(post.id)">
            Delete post
          </button>
        </div>
      </div>
    </div> -->



    <v-card
      class="mx-auto"
      max-width="344"
      variant="outlined"
    >
      <v-card-item>
        <div>
          <div class="text-overline mb-1">
            OVERLINE
          </div>
          <div class="text-h6 mb-1">
            Headline
          </div>
          <div class="text-caption">Greyhound divisely hello coldly fonwderfully</div>
        </div>
      </v-card-item>
  
      <v-card-actions>
        <v-btn variant="outlined">
          Button
        </v-btn>
      </v-card-actions>
    </v-card>
  </template>

<script>

import axios from "axios";

export default {
  name: "Users",
  components: {},
  data() {
    return {
      posts: [],
      /* search: "", */
    };
  },
  methods: {
     getPosts() {
      axios
        .get("http://localhost:8000/posts")
        .then((response) => {
          console.log(response.data);
        })
        .catch((error) => {
          console.log(error.message);
        });
    },


    /* Deletes an entry in the database */
    /* deleteData(id) {
      if (
        confirm(
          "Are you sure you want to delete this user from the database? This choice is permanent and cannot be regretted."
        ) == true
      ) {
        axios
          .delete(`http://localhost:8000/posts/${id}`)
          .then(this.getAllPosts())
          .catch(function (error) {
            console.log(error.response);
          });
      } else {
        return;
      }
    }, */

    /* getAllPosts() {
      axios.get("http://localhost:8000/posts").then((response) => {
        if (this.search) {
          this.posts = response.data.filter(
            (posts) =>
              posts.firstname
                .toLowerCase()
                .includes(this.search.toLowerCase()) ||
              posts.lastname
                .toLowerCase()
                .includes(this.search.toLowerCase()) ||
              posts.title.toLowerCase().includes(this.search.toLowerCase()) ||
              posts.phonenr.toLowerCase().includes(this.search.toLowerCase()) ||
              posts.company.toLowerCase().includes(this.search.toLowerCase()) ||
              posts.department
                .toLowerCase()
                .includes(this.search.toLowerCase()) ||
              posts.system.toLowerCase().includes(this.search.toLowerCase())
          );
        } else {
          console.log(response.data);
          this.posts = response.data;
        }
      });
    }, */
  },
  mounted() {
    console.log("Mounted");
    /* this.getAllPosts(); */
    this.getPosts();
  },
};
</script>