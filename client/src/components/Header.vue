<template>
  <v-toolbar fixed class="light-blue darken-4" dark>
    <v-toolbar-title class="mr-4">
      <router-link
      class="logo"
      tag="span"
      :to="{name: 'songs'}">
      TabTracker
    </router-link>
    </v-toolbar-title>

    <!-- TODO: Implement Me -->
    <v-toolbar-items>
      <v-btn
        flat
        dark
        router to="/songs">
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn
      v-if="!$store.state.isUserLoggedIn"
      flat
      dark
      router to="/login">
      Login
    </v-btn>

    <v-btn
      v-if="!$store.state.isUserLoggedIn"
      flat
      dark
      router to="/register">
      Sign Up
    </v-btn>

    <v-btn
      v-if="$store.state.isUserLoggedIn"
      flat
      dark
      @click="logout">
      Log Out
    </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>
<script>
export default {
  methods: {
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)
      // TODO: redurect to homepage
      this.$router.push({
        name: 'songs'
      })
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
