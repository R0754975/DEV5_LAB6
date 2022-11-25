<script setup>
import { ref, onMounted, reactive } from 'vue';

let messages = reactive({ data: [] });
let comment = ref('');

// onMounted
onMounted(() => {
    
    // fetch video
    const apiUrl = 'https://lab5-p379.onrender.com/api/v1/messages/'
    fetch(apiUrl)
    .then(res => res.json())
    .then(data => {

        messages.data = data;
        console.log (messages.data);
       
    })

});

const addComment = () => {
    const apiUrl = 'https://lab5-p379.onrender.com/api/v1/messages/'
    fetch(apiUrl, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            user: 'Tim',
            text: comment.value
        })
    })
    .then(res => res.json())
    .then(data => {
        messages.data.push({
            user: data.data.user,
            text: data.data.text
        });
        comment.value = '';
    })
}


</script>

<template>
    <div class="messages">
         <ul>
            <li v-for="message in messages.data" >
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
.messages {
    height: 80vh;
    overflow-y: auto;
}



</style>