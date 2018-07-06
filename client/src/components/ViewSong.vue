<template>
  <div>
    <v-layout>
      <v-flex xs6>
        <panel title="Song Metadata">
          <v-layout>
            <v-flex xs6>
              <div class="song-title">
                {{ song.title }}
              </div>
              <div class="song-artist">
                {{ song.artist }}
              </div>
              <div class="song-genre">
                {{ song.genre }}
              </div>

              <v-btn
                dark
                class="cyan"
                :to="{
                  name: 'Song-edit',
                  params () {
                    return {
                      songId: song.id
                    }
                  }
                }">
                Edit
              </v-btn>

              <v-btn
                v-if="isUserLoggedIn"
                dark
                class="cyan"
                @click="bookmark">
                Bookmark
               </v-btn>

              <v-btn
                v-if="isUserLoggedIn"
                dark
                class="cyan"
                @click="unbookmark">
                Unbookmark
              </v-btn>
            </v-flex>

            <v-flex xs6>
              <img class="album-image" :src="song.albumImageUrl">
              <br>
              {{ song.title }}
            </v-flex>
          </v-layout>
        </panel>
      </v-flex>

      <v-flex xs6 class="ml-2">
        <panel title="Youtube Video">
          <youtube
            :video-id="song.youtubeId"
            :player-width="600"
            :player-height="300">
          </youtube>
        </panel>
      </v-flex>

    </v-layout>

    <v-layout class="mt-2">
      <v-flex xs6>
        <panel title="Tabs">
          <v-textarea rows="25" no-resize readonly v-model="song.tab"></v-textarea>
        </panel>
      </v-flex>
      <v-flex xs6 class="ml-2">
        <panel title="Lyrics">
          <v-textarea rows="25" no-resize readonly v-model="song.lyrics"></v-textarea>
        </panel>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import SongsService from '@/services/SongsService'
import { mapState } from 'vuex'

export default {
  data () {
    return {
      song: {}
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn'
    ])
  },
  methods: {
    bookmark () {
      console.log('book')
    },
    unbookmark () {
      console.log('unbook')
    }
  },
  async mounted () {
    const songId = this.$route.params.songId
    this.song = (await SongsService.show(songId)).data
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
    font-size: 30px;
  }

  .song-artist {
    font-size: 24px;
  }

  .song-genre {
    font-size: 18px;
  }

  .album-image {
    width: 100%;
    margin: 0 auto;
  }

  v-textarea {
    width: 100%;
    font-family: monospace;
    border: none;
    height: 600px;
    border-style: none;
    border-color: transparent;
    overflow: auto;
    padding: 40px;
  }
</style>
