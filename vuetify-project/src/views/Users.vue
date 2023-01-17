<template>
    <v-app>
        <div class="d-flex justify-center">
            <v-text-field class="w-50 mx-12"
            prepend-icon="mdi-magnify"
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
            max-width="300"
            variant="outlined"
            :elevation="12"
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
          <div class="text-caption">Behörighet: {{ post.system }}</div>
          <div class="text-caption">Skapad: {{ post.date }}</div>
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
/* import axios from "axios"; */

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

    async deleteData(id) {
      if (
        confirm(
          "Are you sure you want to delete this user from the database? This choice is permanent and cannot be regretted."
        ) == true
      ) {
        try {
          const response = await fetch(`http://localhost:8000/posts/${id}`, 
          { 
          method: "DELETE",
          headers: {
            "Content-Type": "application/json",
          },
        }
        )
        if (!response.ok) {
          throw new Error(`Error ${response.status}`);
        }
        // object was successfully created, do something with the response data
      } catch (error) {
        // there was an error creating the object
        console.log(error);
      }
      
      console.log("Delete succesful", `Post number ID: ${id} is now deleted`);
      this.getAllPosts();
      
    } else {
      return;
      }
    }, 

    async getAllPosts() {
      const response = await fetch(
        "http://localhost:8000/posts"
        )
        const data = await response.json();
        if (this.search) {
          this.posts = data.filter(
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
          console.log(data);
          this.posts = data;
        }
    },
  },

  mounted() {
    console.log("Mounted");
    this.getAllPosts();
  }
};
</script>