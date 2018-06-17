<template>
  <v-app>
    <v-content>
      <page-header/>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
import PageHeader from '@/components/Header.vue'
export default {
  name: 'App',
  components: {
    PageHeader
  }
}
</script>

<style>
.danger-alert {
  color: red;
}

body {
  margin-top: 80px;
}
</style>
