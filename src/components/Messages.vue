<script setup>
import { ref, onMounted, reactive } from 'vue';

let messages = reactive({});

// onMounted
onMounted(() => {
    
    // fetch video
    const apiUrl = 'https://lab5-p379.onrender.com/api/v1/messages/'
    fetch(apiUrl)
    .then(res => res.json())
    .then(data => {

        messages = data;
       
    })

});


</script>

<template>
    <div>
         <ul>
            <li v-for="message in messages" :key="message.id">
                <h3>{{ message.user }}</h3>
                <p>{{ message.text }}</p>
            </li>
        </ul>    
    </div>
    <div>
        <input v-model="comment">
        <button @click="addComment">Add Comment</button>
    </div>
</template>

<style scoped>
</style>