<template>
    <v-layout row>
      <v-flex xs4>
        <panel title="Song Metadata">
          <v-text-field
            required
            :rules="[required]"
            label="Title"
            v-model="song.title"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Artist"
            v-model="song.artist"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Genre"
            v-model="song.genre"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Album"
            v-model="song.album"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Album Image URL"
            v-model="song.albumImageUrl"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Youtube ID"
            v-model="song.youtubeId"></v-text-field>
        </panel>
      </v-flex>

      <v-flex>
        <panel title="Song Structure">
          <v-text-field
            required
            :rules="[required]"
            label="Tab"
            multi-line
            v-model="song.tab"></v-text-field>

          <v-text-field
            required
            :rules="[required]"
            label="Lyrics"
            multi-line
            v-model="song.lyrics"></v-text-field>
        </panel>

        <div class="danger-alert text-xs-center" v-if="error">
          {{error}}
        </div>
        <div class="pr-3 pl-3">
          <v-btn
            dark
            color="primary"
            @click="save">
            Save Song</v-btn>
          <v-btn
            dark
            color="error"
            @click="remove">
            Delete</v-btn>
        </div>
      </v-flex>
    </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'

export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      required: (value) => !!value || 'Required.',
      error: null
    }
  },
  async mounted () {
    try {
      const songId = this.$store.state.route.params.songId
      this.song = (await SongsService.show(songId)).data
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    async save () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all the required fields.'
        return
      }

      try {
        await SongsService.put(this.song)
        const songId = this.$store.state.route.params.songId
        this.$router.push({
          name: 'song',
          params: {
            songId: songId
          }
        })
      } catch (err) {
        console.log(err)
      }
    },

    async remove () {
      try {
        await SongsService.remove(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style scoped>

</style>
