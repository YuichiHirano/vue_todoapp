<template>
  <v-app>
    <v-main>
      <Tasks/>
    </v-main>
  </v-app>
</template>

<script>
import Tasks from './components/Tasks';

export default {
  name: 'App',

  components: {
    Tasks,
  },

  data: () => ({
    //
  }),
};
</script>
