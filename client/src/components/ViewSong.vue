<template>
  <!-- <panel></panel> -->
  <h1>Song</h1>
</template>

<script>
// import Panel from '@/components/Panel'
// import SongsService from '@/services/SongsService'
export default {
  async mounted () {
    const songId = this.$store.state.route.params.songId
    // const song = await SongsService.show(songId)
    console.log(songId)
  }
}
</script>

<style scoped>

</style>
