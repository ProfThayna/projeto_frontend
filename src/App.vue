<template>
  <v-app>
    <v-app-bar
      app
      color="purple"
      dark
    >
    </v-app-bar>

    <v-main>
      <ProfileTemplate/>
    </v-main>
  </v-app>
</template>

<script>
import ProfileTemplate from './components/ProfileTemplate.vue';

export default {
  name: 'App',

  components: {
    ProfileTemplate
  },

  data: () => ({
    //
  }),
};
</script>
