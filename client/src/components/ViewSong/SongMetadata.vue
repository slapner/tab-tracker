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
        :to="{
          name: 'song-edit',
          params () {
            return {
              songId: song.id
            }
          }
        }">
        Edit
      </v-btn>
      <v-btn
        v-if="isUserLoggedIn && !bookmark"
        color="primary"
        dark
        small
        @click="setAsBookmark">
        Set As Bookmark
      </v-btn>
      <v-btn
        v-if="isUserLoggedIn && bookmark"
        color="primary"
        dark
        small
        @click="unsetAsBookmark">
        Unset As Bookmark
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
import {mapState} from 'vuex'
import BookmarksService from '@/services/BookmarksService'

export default {
  data () {
    return {
      bookmark: null
    }
  },
  props: [
    'song'
  ],
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  watch: {
    async song () {
      if (!this.isUserLoggedIn) {
        return
      }

      try {
        this.bookmark = (await BookmarksService.index({
          songId: this.song.id,
          userId: this.user.id
        })).data
      } catch (err) {
        console.log(err)
      }
    }
  },
  methods: {
    async setAsBookmark () {
      try {
        this.bookmark = (await BookmarksService.post({
          songId: this.song.id,
          userId: this.user.id
        })).data
      } catch (err) {
        console.log(err)
      }
    },
    async unsetAsBookmark () {
      try {
        await BookmarksService.delete(this.bookmark.id)
        this.bookmark = null
      } catch (err) {
        console.log(err)
      }
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
