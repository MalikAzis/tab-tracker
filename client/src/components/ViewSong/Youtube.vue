<template>
  <panel title="YouTube Video" class="ml-2">
  <!-- youtube embedded -->
  <youtube class="youtube"
    :video-id="youtubeId"
    :player-width="500"
    :player-height="285">
    </youtube>
  </panel>
</template>

<script>
export default {
  props: [
    'youtubeId'
  ]
}
</script>

<style scoped>
  #player {
    width: 150%;
  }
</style>
