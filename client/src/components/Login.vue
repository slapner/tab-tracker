<template>
  <v-container fluid fill-height>
    <v-layout align-center justify-center>
      <v-flex xs6>
        <div class="white elevation-2">
          <v-toolbar flat dense dark color="cyan">
            <v-toolbar-title>Login</v-toolbar-title>
          </v-toolbar>

          <div class="pl-4 pr-4 pt-2 pb-2">
            <form name="tab-tracker-form">
              <v-text-field
                type="email"
                name="email"
                v-model="email"
                label="Email"></v-text-field>

              <v-text-field
                type="password"
                name="password"
                v-model="password"
                label="Password"></v-text-field>

              <div v-html="error" class="error"/>
              <v-btn
                block dark
                color="cyan"
                @click="login">Login</v-btn>
            </form>
          </div>

        </div>
      </v-flex>
    </v-layout>
  </v-container>
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
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  color: red;
}
</style>
