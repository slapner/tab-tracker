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
            block
            color="primary"
            @click="create">
            Create Song</v-btn>
        </div>
      </v-flex>
    </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
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
  components: {
    Panel
  },
  methods: {
    async create () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all the required fields.'
        return
      }

      try {
        await SongsService.post(this.song)
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
