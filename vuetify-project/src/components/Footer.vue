<template>
    <v-app>
        <v-footer :elevation="5"
            class="bg-black-1 text-center d-flex flex-column mt-4"
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
        
            <v-divider></v-divider>
        
            <div>
              {{ new Date().getFullYear() }} — <strong>Vuetify, OnifyForms</strong>
            </div>
          </v-footer>
    </v-app>
</template>

<script>
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
</script>

<style>

.v-footer {
    position: fixed;
    bottom: 0;
}

</style>