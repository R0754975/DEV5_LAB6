<script setup>
import { ref, onMounted, reactive } from 'vue';
import 'animate.css';    

let videoSrc = ref('');
let counter = ref(0);
let videos = reactive({data: []});
let animation = ref('');

    // onMounted
    onMounted(() => {
        
        // fetch video
        const apiUrl = 'https://app.fakejson.com/q/Yt0OWPDd?token=exRU8ChVAvPcxabJNQxtAw'
        fetch(apiUrl)
        .then(res => res.json())
        .then(data => {

            videoSrc.value = data.videos[0].video;

            videos.data = data.videos;

            console.log(videos);


        })

    });


    const next = () => {
        if (counter.value < videos.data.length - 1) {
            animation.value = 'animate__fadeOut';
            setTimeout(() => {
                animation.value = 'animate__fadeIn';
                counter.value++;
                videoSrc.value = videos.data[counter.value].video;
            }, 500);       
        }
    }

    const back = () => {
        if (counter.value > 0) {
            animation.value = 'animate__fadeOut';
            setTimeout(() => {
                animation.value = 'animate__fadeIn';
                counter.value--;
                videoSrc.value = videos.data[counter.value].video;
            }, 500);
        }
    }



</script>

<template>
  <div class="blurr">
    <div class="controls">
        <a @click.prevent="back" href="#">B</a>
        <a @click.prevent="next" href="#">N</a>
    </div>
    <video
    :src="videoSrc"
    :class="animation"
    class="animate__animated"
    autoplay
    muted
    ></video>
  </div>

</template>

<style scoped>

.controls {
    position:absolute;
    top: 0;
    right: 0;
    height: 100%;
    display: flex;
    align-items: center;
    z-index: 1;
}

.controls a {
   color:white;
   padding: 1em;
   text-decoration: none;
   font-size: 2em;

}

video {
    width: 100%;
    height: 100vh;
}

.blurr {
    background-image: url("./src/assets/background.jpg");
    background-size: cover;
    position: relative;
}

</style>
