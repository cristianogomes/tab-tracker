<template>
  <v-layout colum>
    <v-flex xs6 offset-xs3>
      <panel title="Songs">
        <v-btn slot="action" fab light small absolute right middle class="cyan accent-2"
          @click="navigateTo({name: 'songs-create'})">
          <v-icon>add</v-icon>
        </v-btn>

        <div v-for="song in songs" :key="song.id" class="song">
          <v-layout>
            <v-flex xs6>
              <div class="song-tilte">
                {{song.title}}
              </div>

              <div class="song-artist">
                {{song.artist}}
              </div>

              <div class="song-genre">
                {{song.album}}
              </div>

              <v-btn dark class="cyan" @click="navigateTo({name:'song', params: {songId: song.id}})">View</v-btn>
            </v-flex>

            <v-flex xs6>
              <img class="album-image" :src="song.albumImage"/>
            </v-flex>
          </v-layout>
        </div>
      </panel>
    </v-flex>
  </v-layout>
</template>

<script>
  import SongService from '@/services/SongsService'
  import Panel from '@/components/Panel'

  export default {
    data () {
      return {
        songs: null
      }
    },
    methods: {
      navigateTo (route) {
        this.$router.push(route)
      }
    },
    async mounted () {
      this.songs = (await SongService.index()).data
    },
    components: {
      Panel
    }
  }
</script>

<style scoped>
  .song {
    padding: 20px;
    height: 330px;
    overflow: hidden;
  }

  .song-tilte{
    font-size: 30px;
  }
  
  .song-artist{
    font-size: 24px;
  }
  
  .song-genre{
    font-size: 18px;
  }

  .album-image {
    width: 70%;
    margin: 0 auto;
  }
</style>
