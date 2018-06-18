<template>
  <v-toolbar dark color="primary" fixed>
    <v-toolbar-side-icon></v-toolbar-side-icon>
    <v-toolbar-title class="white--text">
      <router-link
        class="title pr-4"
        tag="span"
        :to="{
          name: 'songs'
        }">
        TabTracker
      </router-link>
    </v-toolbar-title>

    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat
        :to="{
          name: 'songs'
        }">
        Browse
      </v-btn>
    </v-toolbar-items>

    <v-spacer></v-spacer>

    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat
        v-if="!$store.state.isUserLoggedIn"
        :to="{
          name: 'login'
        }">
        Login
      </v-btn>

      <v-btn flat
        v-if="!$store.state.isUserLoggedIn"
        :to="{
          name: 'register'
        }">
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
    logout () {
      this.$store.dispatch('setToken', null)
      this.$store.dispatch('setUser', null)

      this.$router.push({
        name: 'songs'
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
