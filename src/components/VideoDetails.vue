<script setup>
import { ref, onMounted } from 'vue';

let username = ref('');
let description = ref('');


// onMounted
onMounted(() => {
    
    // fetch video
    const apiUrl = 'https://app.fakejson.com/q/Yt0OWPDd?token=exRU8ChVAvPcxabJNQxtAw'
    fetch(apiUrl)
    .then(res => res.json())
    .then(data => {

        console.log(data);

        username.value = data.videos[0].username;
        description.value = data.videos[0].description;
    })

});

</script>

<template>
  <div>
    <h3>{{ username }}</h3>
    <p>{{ description }}</p>
  </div>

</template>

<style scoped>

div {
    padding: 0 2em;
}

</style>
