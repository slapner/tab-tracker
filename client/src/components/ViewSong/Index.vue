<template>
  <v-container fluid>
    <v-layout row>
      <v-flex xs6>
        <song-metadata :song="song"></song-metadata>
        <tab :song="song" />
      </v-flex>
      <v-flex xs6>
        <you-tube :youtubeId="song.youtubeId" />
        <lyrics :song="song"></lyrics>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import Panel from '@/components/Panel'
import SongsService from '@/services/SongsService'
import SongMetadata from '@/components/ViewSong/SongMetadata'
import YouTube from '@/components/ViewSong/YouTube'
import Lyrics from '@/components/ViewSong/Lyrics'
import Tab from '@/components/ViewSong/Tab'

export default {
  components: {
    Panel,
    SongMetadata,
    YouTube,
    Lyrics,
    Tab
  },
  data () {
    return {
      song: {}
    }
  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    this.song = (await SongsService.show(songId)).data
  }
}
</script>

<style scoped>

</style>
