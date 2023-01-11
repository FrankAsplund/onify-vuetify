<template>
  <Navbar />
    <v-app>
      <router-view />
    </v-app>
  <Footer /> 
</template>

<script setup>
  import Navbar from './components/Navbar.vue';
  import Footer from './components/Footer.vue';
  import { RouterLink, RouterView } from "vue-router";
</script>
