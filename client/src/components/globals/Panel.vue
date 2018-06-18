<template>
  <v-container>
    <v-layout row>
      <v-flex>
        <div class="white elevation-2">
          <v-toolbar flat dense dark color="cyan">
            <v-toolbar-title>{{ title }}</v-toolbar-title>
            <slot name="action" />
          </v-toolbar>
          <div class="pt-2 pb-2 pr-4 pl-4">

            <slot>
              No slot content defined.
            </slot>
          </div>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  props: [
    'title'
  ]
}
</script>

<style scoped>

</style>
