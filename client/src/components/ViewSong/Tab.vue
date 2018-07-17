<template>
  <panel title="Tabs" class="mt-2 ml-2">
    <textarea
      readonly
      v-model="song.tab"
    ></textarea>
  </panel>
</template>

<script>
export default {
  props: [
    'song'
  ]
}
</script>

<style scoped>

textarea {
  width: 100%;
  height: 285px;
  text-align: justify;
  font-family: monospace;
  border-style: none;
  border-color: transparent;
  overflow: auto;
  padding: 40px;
}
</style>
