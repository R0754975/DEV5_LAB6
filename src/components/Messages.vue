<script setup>

</script>

<template>
    <div>
         <ul>
            <li v-for="message in messages" :key="message.id">
                <h3>{{ message.username }}</h3>
                <p>{{ message.message }}</p>
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