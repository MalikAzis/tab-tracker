<template>
  <panel title="Song Metadata">
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
        dark
        color="light-blue darken-4"
        @click="setAsBookmark">
        Bookmark
      </v-btn>

      <v-btn
        v-if="isUserLoggedIn && bookmark"
        dark
        color="light-blue darken-4"
        @click="unsetAsBookmark">
        Unbookmark
      </v-btn>
      </v-flex>

      <v-flex xs6>
        <img :src="song.albumImageUrl" class="album-image">
        <br>
        {{song.album}}
      </v-flex>
    </v-layout>
  </panel>
</template>

<script>
import {mapState} from 'vuex'
import BookmarkService from '@/services/BookmarkService'

export default {
  props: [
    'song'
  ],
  data () {
    return {
      bookmark: null
    }
  },
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
        const bookmarks = (await BookmarkService.index({
          songId: this.song.id,
          userId: this.user.id
        })).data
        if (bookmarks.length) {
          this.bookmark = bookmarks[0]
        }
      } catch (err) {
        console.log(err)
      }
    }
  },
  methods: {
    async setAsBookmark () {
      try {
        this.bookmark = (await BookmarkService.post({
          songId: this.song.id,
          userId: this.user.id
        })).data
      } catch (err) {
        console.log(err)
      }
    },
    async unsetAsBookmark () {
      try {
        await BookmarkService.delete(this.bookmark.id)
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
  padding: 20px;
  height: 330px;
  overflow: hidden;
}

.song-title {
  font-size: 24px;
  font-weight: bold;
}

.song-artist {
  font-size: 18px;
}

.song-genre {
  font-size: 15px;
}

.album-image {
  width: 60%;
  margin: 0 auto;
}

</style>
