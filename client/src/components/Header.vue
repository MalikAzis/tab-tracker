<template>
  <v-toolbar fixed class="light-blue darken-4" dark>
    <v-toolbar-title class="mr-4">
      <span class="logo" @click="navigateTo({name: 'root'})">TabTracker</span>
    </v-toolbar-title>

    <!-- TODO: Implement Me -->
    <!-- <v-toolbar-items>
      <v-btn flat dark>
        Browse
      </v-btn>
    </v-toolbar-items> -->

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn
      v-if="!$store.state.isUserLoggedIn"
      flat
      dark
      router to="login">
      Login
    </v-btn>
    </v-toolbar-items>

    <v-toolbar-items>
      <v-btn
      v-if="!$store.state.isUserLoggedIn"
      flat
      dark
      router to="register">
      Sign Up
    </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>
<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .logo {
    cursor: pointer;
  }

</style>
