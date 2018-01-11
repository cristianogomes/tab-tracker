<template>
   <v-layout colum>
    <v-flex xs6 offset-xs3>
      <panel title="Login">
        <form name="tab-tracker-form">
          <v-text-field type="email" name="email" label="Email" v-model="email"/>
          <br/>

          <v-text-field type="password" name="password" label="Password" v-model="password"/>
          <div v-html="error"/>
          <br/>

          <v-btn @click="login" dark class="cyan">Login</v-btn>
        </form>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  import Panel from '@/components/Panel'

  export default {
    data () {
      return {
        email: '',
        password: '',
        error: null
      }
    },
    methods: {
      async login () {
        try {
          const response = await AuthenticationService.login({
            email: this.email,
            password: this.password
          })
          this.$store.dispatch('setToken', response.data.token)
          this.$store.dispatch('setUser', response.data.user)
        } catch (error) {
          this.error = error.response.data.error
        }
      }
    },
    components: {
      Panel
    }
  }
</script>

<style scoped>
  .error {
    color: red;
  }
</style>
