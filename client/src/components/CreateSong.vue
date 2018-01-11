<template>
  <v-layout>
    <v-flex xs4>
      <panel title="Song Metadata">
        <v-text-field label="Title" v-model="song.title"
          required :rules="[required]"/>
        <v-text-field label="Artist" v-model="song.artist"
          required :rules="[required]"/>
        <v-text-field label="Genre" v-model="song.genre"
          required :rules="[required]"/>
        <v-text-field label="Album" v-model="song.album"
          required :rules="[required]"/>
        <v-text-field label="Album Image URL" v-model="song.albumImage"
          required :rules="[required]"/>
        <v-text-field label="Youtube ID" v-model="song.youtubeId"
          required :rules="[required]"/>
      </panel>
    </v-flex>

    <v-flex xs8>
        <panel title="Song" class="ml-2">
          <v-text-field label="Tab" multi-line v-model="song.lyrics" 
            required :rules="[required]"/>
          <v-text-field label="Lyrics" multi-line v-model="song.tab"
            required :rules="[required]"/>
        </panel>

        <div class="danger-alert" v-if="error">
          {{error}}
        </div>
        <v-btn dark class="cyan" @click="create">Create Song</v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
  import SongsService from '@/services/SongsService'
  import Panel from '@/components/Panel'

  export default {
    data () {
      return {
        song: {
          title: null,
          artist: null,
          genre: null,
          album: null,
          albumImage: null,
          youtubeId: null,
          lyrics: null,
          tab: null
        },
        error: null,
        required: (value) => !!value || 'Required.'
      }
    },
    methods: {
      async create () {
        this.error = null
        const areAllFieldsFilledIn = Object.keys(this.song).every(key => !!this.song[key])
        if (!areAllFieldsFilledIn) {
          this.error = 'Informe todos os campos'
          return
        }
        try {
          await SongsService.post(this.song)
          this.$router.push({
            name: 'songs'
          })
        } catch (error) {
          console.log(error)
        }
      }
    },
    components: {
      Panel
    }
  }
</script>

<style>

</style>
