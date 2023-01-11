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

<style>

.v-application__wrap {
    backface-visibility: hidden;
    display: flex;
    flex-direction: column;
    flex: 1 1 auto;
    max-width: 100%;
    min-height: 20vh;
    position: static;
}

</style>
