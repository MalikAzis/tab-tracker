<template>
  <panel title="Songs">
    <v-btn
      slot="action"
      light
      medium
      absolute
      right
      middle
      fab
      @click="navigateTo({name: 'songs-create'})"
      >
      <v-icon>add</v-icon>
    </v-btn>

    <div
    v-for="song in songs"
    class="song"
    :key="song.id">

      <v-layout>
        <v-flex xs6>
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
          color="light-blue darken-4"
          @click="navigateTo({
            name: 'song',
            params: {
              songId: song.id
            }
          })">
          View Song
        </v-btn>
        </v-flex>

        <v-flex xs6>
          <img :src="song.albumImageUrl" class="album-image">
        </v-flex>
      </v-layout>
    </div>
  </panel>
</template>

<script>
import SongService from '@/services/SongService'
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
  watch: {
    '$route.query.search': {
      immediate: true,
      async handler (value) {
        this.songs = (await SongService.index(value)).data
      }
    }
  }
}
</script>

<style scoped>

.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 24px;
  font-weight: bold;
}

.song-artist {

}

.song-genre {

}

.album-image {
  width: 70%;
  margin: 0 auto;
}
</style>
