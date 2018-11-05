<template>
 <v-app id="app">
  <login isOpen = "true">
  </login>
  <homepage v-if ="homepage"></homepage>
  </v-app>
</template>

<script>

import login from './components/login.vue';
import homepage from './components/homepage.vue';


export default {
  name: 'app',
  components: {
    login,
    homepage,
  },
  data: () => ({login:true,
  homepage: true,
   
  }),
};

</script>

<style>
body, html{
  height: 100%;
  font-family: 'Roboto'!important;
  font-weight: 300!important;
}
.title{
  font-weight: 300!important;
}

</style>
