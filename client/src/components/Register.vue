<template>
  <v-layout row >
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar flat dense class="cyan" dark>
          <v-toolbar-tittle>Register</v-toolbar-tittle>
        </v-toolbar>

        <div class="pl-4 pr-4 pt-2 pb-2">
          <input type="email"
          v-model="email"
          name="email"
          placeholder="email">
          <br>
          <input type="password"
          v-model="password"
          name="password"
          placeholder="password">
          <br>
          <div class="error" v-html="error">
          </div>
          <br>
          <button type="button"
          name="submit"
          @click="register">
          Register
          </button>
        </div>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  color: red;
}
</style>
