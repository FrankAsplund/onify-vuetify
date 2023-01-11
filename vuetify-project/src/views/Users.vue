<template>
    <v-app>

        <div class="d-flex justify-center">
            <v-text-field class=" w-50 mx-12"
            variant="outlined"
              type="text"
              v-model.trim="search"
              placeholder="Search for users..."
              @keyup="getAllPosts">
            </v-text-field>
        </div>

        <div class="d-flex align-content-space-between flex-wrap ma-4 pa-2"
        >
            <v-card
            v-for="post in posts" 
            :key="post.id" 
            class="ma-2 pa-2"
            min-width="300"
            variant="outlined"
            >
            <v-card-subtitle> {{ post.id }} </v-card-subtitle>
            <v-card-item>
            <div>
                <div class="text-h6 mb-1"> {{ post.firstname }} {{ post.lastname }} </div>
                
                <div class="text-overline mb-1"> Titel: {{ post.title }} </div>
          <!-- Byt ut alla rubriker mot symboler -->
          <div class="text-caption">Telefonnummer: {{ post.phonenr }}</div>
          <div class="text-caption">Bolag: {{ post.company }}</div>
          <div class="text-caption">Avdelning: {{ post.department }}</div>
          <div class="text-caption">Behörighet: blablabla</div>
          </div>
            </v-card-item>
    <v-card-actions>
        <v-btn 
        variant="tonal"  
        color="red"
        @click="deleteData(post.id)"
        > Delete user </v-btn>
    </v-card-actions>
        </v-card>
        </div>
    </v-app>
</template>

<script>
import axios from "axios";

export default {
    name: "Users",
    components: {},
    data() {
        return {
            posts: [],
            search: ""
    };
  },
  methods: {
     /* getPosts() {
      axios
        .get("http://localhost:8000/posts")
        .then((response) => {
          console.log(response.data);
          this.posts = response.data;
        })
        .catch((error) => {
          console.log(error.message);
        });
    }, */


    /* Deletes an entry in the database */
    deleteData(id) {
      if (
        confirm(
          "Are you sure you want to delete this user from the database? This choice is permanent and cannot be regretted."
        ) == true
      ) {
        axios
          .delete(`http://localhost:8000/posts/${id}`)
          .then((response) => {
            this.posts = response.data;
          })
          .catch(function (error) {
            console.log(error.response);
          });
      } else {
        return;
      }
    },

    getAllPosts() {
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
                .includes(this.search.toLowerCase())
          );
        } else {
          console.log(response.data);
          this.posts = response.data;
        }
      });
    },
  },

  mounted() {
    console.log("Mounted");
    this.getAllPosts();
    /* this.getPosts(); */
  }

};
</script>