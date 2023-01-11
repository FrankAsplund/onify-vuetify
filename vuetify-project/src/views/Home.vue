<!-- <template>
  <main>
    <v-app-bar :elevation="5">
      <img
        alt="logo"
        class="mx-2 px-2"
        src="https://8128125.fs1.hubspotusercontent-na1.net/hub/8128125/hubfs/onify-logo-white-1.png?width=136&name=onify-logo-white-1.png"
        width="136"
        height="50"
      />
      <v-app-bar-title>Onify forms</v-app-bar-title>

      <div class="router">
        <v-btn variant="tonal" class="mx-2">
          <RouterLink to="/">Home</RouterLink>
</v-btn>
<v-btn variant="tonal" class="mx-2">
  <RouterLink to="/users">Users</RouterLink>
</v-btn>
      </div>
  
    <v-btn icon="mdi-heart"></v-btn>

    <v-btn icon="mdi-magnify"></v-btn>

    <v-btn icon="mdi-dots-vertical"></v-btn>
</v-app-bar> -->

<template>
    <v-app>
  <div class="d-flex align-center flex-row ma-4 pa-2">
    <v-card variant="tonal" class="mt-5 mb-8 rounded-sm" width="400">
    <v-card-title>
      Skapa användare
    </v-card-title>
      <v-card-text>
        Här kan du skapa dina egna användare, komplett med namn, titel, företag, och allt annat du skulle tänka dig!
      </v-card-text> 
  </v-card>
</div>

<div class="mx-12 my-4 pa-6 rounded-xl bg-grey-darken-2">
  <OnifyForm />
</div>

 <!--  <v-footer :elevation="5"
    class="bg-black-1 text-center d-flex flex-column"
  >
    <div>
      <v-btn
        v-for="icon in icons"
        :key="icon"
        class="mx-4"
        :icon="icon"
        variant="text"
      ></v-btn>
    </div>

    <div class="pt-0">
      Phasellus feugiat arcu sapien, et iaculis ipsum elementum sit amet. Mauris cursus commodo interdum. Praesent ut risus eget metus luctus accumsan id ultrices nunc. Sed at orci sed massa consectetur dignissim a sit amet dui. Duis commodo vitae velit et faucibus. Morbi vehicula lacinia malesuada. Nulla placerat augue vel ipsum ultrices, cursus iaculis dui sollicitudin. Vestibulum eu ipsum vel diam elementum tempor vel ut orci. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
    </div>

    <v-divider></v-divider>

    <div>
      {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
    </div>
  </v-footer> -->
</v-app>
</template>

<!-- <script>
  export default {
    data: () => ({
      icons: [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ],
    }),
  }
</script> -->

<script setup>
import OnifyForm from "../components/OnifyForm.vue"
import { RouterLink, RouterView } from "vue-router";
</script>

<style>
a {
  text-decoration: none !important;
  background-color: transparent !important;
  text-decoration-color: white !important;
  color: white;
}

a:visited { 
 text-decoration: none !important;
 color: white; 
}
</style>
