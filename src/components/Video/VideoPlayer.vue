<script setup>
import { ref, reactive, onMounted } from 'vue'; 

//define emits
const emit = defineEmits(['update:videoDescription']); //emits voor communicatie tussen componenten

let videoUrl = ref('');
let videos = reactive({
    data: [],
});

onMounted(() => {
    fetch('https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15')
        .then(response => response.json())
        .then(data => {
            console.log('API response:', data);
            videos.data = data.record.videos;
            videoUrl.value = videos.data[0].video;
            emit('update:videoDescription', videos.data[0].description);
            console.log('videos.data:', videos.data);
            console.log('videoUrl:', videoUrl.value);
        })
        .catch(error => {
            console.error('Error fetching video data:', error);
        });
});

</script>

<template>
  <!--VideoPlayer.vue-->
  <div>
    <video :src="videoUrl" controls autoplay muted loop></video>
  </div>
</template>

<style scoped>
 /*scoped wil zeggen specifiek voor component*/
</style>
