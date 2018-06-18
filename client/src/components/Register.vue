<template>
  <v-container fluid fill-height class="negative-margin">
    <v-layout align-center justify-center>
      <v-flex xs6>
        <div class="white elevation-2">
          <v-toolbar flat dense dark color="cyan">
            <v-toolbar-title>Register</v-toolbar-title>
          </v-toolbar>

          <div class="pl-4 pr-4 pt-2 pb-2">
            <form name="tab-tracker-form" autocomplete="off">
              <v-text-field
                type="email"
                name="email"
                v-model="email"
                autocomplete="off"
                label="Email"></v-text-field>

              <v-text-field
                name="password"
                v-model="password"
                :append-icon="e1 ? 'visibility' : 'visibility_off'"
                :append-icon-cb="() => (e1 =!e1)"
                :type="e1 ? 'password' : 'text'"
                label="Password"></v-text-field>

              <v-alert v-model="hasError" type="error" dismissible>
                {{error}}
              </v-alert>

              <v-btn
                block dark
                color="cyan"
                @click="register">Register</v-btn>
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
      e1: true,
      error: null,
      hasError: false
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        this.$router.push({
          name: 'songs'
        })
      } catch (error) {
        this.error = error.response.data.error
        this.hasError = true
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.negative-margin {
  margin-top: -80px;
}
</style>
