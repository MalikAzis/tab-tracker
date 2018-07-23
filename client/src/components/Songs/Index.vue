<template>
  <v-form>
    <v-container>
      <v-layout row wrap>
        <v-flex xs-6>
          <songs-bookmarks/>
        </v-flex>

        <v-flex xs6 >
          <songs-search-panel/>
          <songs-panel class="mt-2"/>
        </v-flex>
        </v-layout>
    </v-container>
  </v-form>
</template>

<script>
import SongsPanel from './SongsPanel'
import SongsBookmarks from './SongsBookmarks'
import SongsSearchPanel from './SongsSearchPanel'
import SongService from '@/services/SongService'
export default {
  components: {
    SongsPanel,
    SongsSearchPanel,
    SongsBookmarks
  },
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
