<template>
  <panel title="Songs">
    <v-btn
      slot="action"
      fab
      medium
      light
      absolute
      right
      middle
      color="cyan"
      :to="{
        name: 'songs-create'
      }"
      class="accent-2">
      <v-icon>add</v-icon>
    </v-btn>
    <div v-for="song in songs" :key="song.id" class="song">
      <v-layout row>
        <v-flex xs6 class="text-xs-center">
          <div class="song-title">
            {{song.title}}
          </div>
          <div class="song-artist">
            {{song.artist}}
          </div>
          <div class="song-genre">
            {{song.genre}}
          </div>
          <v-btn
            dark
            color="primary"
            :to="{
              name: 'song',
              params: {
                songId: song.id
              }
            }">
            View
          </v-btn>
        </v-flex>
        <v-flex xs6>
          <img class="album-image" alt="" v-bind:src="song.albumImageUrl">
        </v-flex>
      </v-layout>
    </div>
  </panel>
</template>

<script>
import SongsService from '@/services/SongsService'

export default {
  data () {
    return {
      songs: null
    }
  },
  watch: {
    '$route.query.search': {
      immediate: true,
      async handler (value) {
        this.songs = (await SongsService.index(value)).data
      }
    }
  }
}
</script>

<style scoped>
body {
  margin-top: 80px;
}

.song {
  padding: 20px;;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 30px;
}

.song-artist {
  font-size: 24px;
}

.song-genre {
  font-size: 18px;
}
.album-image {
  width: 70%;
  margin: 0 auto;
}
</style>
