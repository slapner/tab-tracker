<template>
<panel title="Song Metadata">
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
        color="primary"
        dark
        small
        @click="navigateTo({
          name: 'song-edit',
          params: {
            songId: song.id
          }
        })">
        Edit
        </v-btn>
    </v-flex>
    <v-flex xs6 class="text-xs-center">
      <img class="album-image" alt="" v-bind:src="song.albumImageUrl">
      <div>{{song.album}}</div>
    </v-flex>
  </v-layout>
</panel>
</template>

<script>
import Panel from '@/components/Panel'

export default {
  components: {
    Panel
  },
  props: [
    'song'
  ],
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>
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
