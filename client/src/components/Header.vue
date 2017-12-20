<template>
  <v-toolbar fixed dark class="cyan">
    <v-toolbar-title class="mr-4" to="root">
      <v-btn flat dark router to="/">TabTracker</v-btn>
    </v-toolbar-title>

    <v-toolbar-items>
      <v-btn flat dark>Browser</v-btn>
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
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
  export default {
  }
</script>

<style scoped>
</style>
