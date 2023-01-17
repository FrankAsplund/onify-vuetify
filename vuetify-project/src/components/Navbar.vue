<template>
<v-app >
      <v-app-bar :elevation="5" class="fixed">
        <img
          alt="logo"
          class="mx-2 px-2"
          src="https://8128125.fs1.hubspotusercontent-na1.net/hub/8128125/hubfs/onify-logo-white-1.png?width=136&name=onify-logo-white-1.png"
          width="145"
          height="50"
        />
  
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
      </v-app-bar>
</v-app>
</template>
    

<script>

/* export default navbar; */

</script>

<style>
.fixed {
    position: fixed;
    top: 0;
}

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