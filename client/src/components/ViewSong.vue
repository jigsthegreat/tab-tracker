<template>

</template>

<script>
import SongsService from '@/services/SongsService'

export default {
  name: 'Blank',
  data () {
    return {
      song: null
    }
  },
  methods: {

  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    this.song = await SongsService.show(songId)
  }
}
</script>

<style scoped>

</style>
