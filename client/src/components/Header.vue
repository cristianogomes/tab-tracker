<template>
  <v-toolbar fixed dark class="cyan">
    <v-toolbar-title class="mr-4" to="root">
      <v-btn flat dark router to="/">TabTracker</v-btn>
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn flat dark router to="songs">
        Browser
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items>
      <v-btn flat dark router to="login"
        v-if="!$store.state.isUserLoggedIn">
        Login
      </v-btn>
      <v-btn flat dark router to="register"
        v-if="!$store.state.isUserLoggedIn">
          Sign Up
      </v-btn>
      <v-btn flat dark router @click="logout"
        v-if="$store.state.isUserLoggedIn">
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
        this.$router.push({
          name: 'root'
        })
      }
    }
  }
</script>

<style scoped>
</style>
