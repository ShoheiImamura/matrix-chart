<template>
  <v-app>
    <v-app-bar app dark> </v-app-bar>

    <v-main>
      <MatrixChart />
    </v-main>
  </v-app>
</template>

<script>
import MatrixChart from "./components/MatrixChart";

export default {
  name: "App",

  components: {
    MatrixChart,
  },

  data: () => ({
    //
  }),
};
</script>
