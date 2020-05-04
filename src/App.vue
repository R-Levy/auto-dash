<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h2>Client Dashboard</h2>
      </div>
    </v-app-bar>

    <v-content>
      <api-list />
    </v-content>
  </v-app>
</template>

<script>
import ApiList from "./components/ApiList";

export default {
  name: "App",

  components: {
    ApiList
  },

  data: () => ({
    //
  })
};
</script>
