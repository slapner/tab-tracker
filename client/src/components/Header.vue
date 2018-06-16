<template>
  <v-toolbar dark color="primary" fixed>
    <v-toolbar-side-icon></v-toolbar-side-icon>
    <v-toolbar-title class="white--text">
      <span
        class="title pr-4"
        @click="navigateTo({ name: 'root' })">
        TabTracker
      </span>
    </v-toolbar-title>

    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat
        @click="navigateTo({ name: 'songs' })">
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat
        v-if="!$store.state.isUserLoggedIn"
        @click="navigateTo({ name: 'login' })">
        Login
      </v-btn>

      <v-btn flat
        v-if="!$store.state.isUserLoggedIn"
        @click="navigateTo({ name: 'register' })">
        Sign Up
      </v-btn>

      <v-btn flat
        v-if="$store.state.isUserLoggedIn"
        @click="logout">
        Log Out
      </v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    },
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
.title:hover {
  cursor: pointer;
}
</style>
