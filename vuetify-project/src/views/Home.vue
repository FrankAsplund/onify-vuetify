<template>
  <v-app>
    <!-- <div class="d-flex align-center flex-row ma-4 pa-2">
      <v-card variant="tonal" class="mt-5 mb-8 rounded-sm" width="400">
        <v-card-title>Skapa användare</v-card-title>
      <v-card-text>
        Här kan du skapa dina egna användare, komplett med namn, titel, företag, och allt annat du skulle tänka dig!
      </v-card-text> 
      </v-card>
    </div> -->

<div class="mx-12 my-2 pa-6 rounded-m bg-grey-darken-4" :elevation="12">
  <OnifyForm />
</div>

</v-app>
</template>

<script setup>
import OnifyForm from "../components/OnifyForm.vue"
/* import { RouterLink, RouterView } from "vue-router"; */
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
