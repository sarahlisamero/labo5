<script setup>

import VideoPlayer from './components/Video/VideoPlayer.vue';
import VideoDetails from './components/Video/VideoDetails.vue';
import Chat from './components/Chat/Chat.vue';

import { ref } from 'vue'; 
let newDescription = ref('Default title');

const updateVideo = (description) => {
  newDescription.value = description;
}

</script>

<template>
  <!--App.vue-->
  <div class="tiktok">
    <div>
      <VideoPlayer @update:video-description="updateVideo"/> <!--camelCase wordt in emits een steepje (-)-->
      <!--<VideoPlayer @update:video_description="updateVideo"/>-->
    </div>
    <div>
      <VideoDetails :description="newDescription"/>
      <Chat/>
    </div>
  </div>
</template>

<style scoped>
 /*scoped wil zeggen specifiek voor component*/
 .tiktok{
  display: grid;
  grid-template-columns: 1fr 1fr;
 }
</style>
