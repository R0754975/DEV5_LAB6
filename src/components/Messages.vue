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
    <div class="comment">
        <input v-model="comment">
        <button @click="addComment">Add Comment</button>
    </div>
</template>

<style scoped>
.messages {
    height: 80vh;
    overflow-y: auto;
    padding-left: 5%;
}

.messages ul {
    padding-left: 0;
}

.comment {
    padding-left: 5%;
}

li {
    list-style: none;
    border-bottom: 1px solid #ccc;
}

.comment button {
    margin-left: 2%;
    background-color: rgb(47, 46, 46);
    border: none;
    color: white;
    border-radius: 5px;
    padding: 5px;
}

.comment input {
    padding: 3px;
}


</style>