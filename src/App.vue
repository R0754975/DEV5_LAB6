<script setup>
  import VideoPlayer from './components/VideoPlayer.vue'
  import VideoDetails from './components/VideoDetails.vue'
  import Messages from './components/Messages.vue'
</script>

<template>
  <div class="app">
    <VideoPlayer />
    <div>
      <VideoDetails />
      <Messages />
    </div>  
  </div>
</template>

<style scoped>

.app {
  display: grid;
  grid-template-columns: 8fr 4fr;
}

</style>
