<script setup>
//define properties
const props = defineProps(["description"]);
</script>

<template>
  <!--VideoDetails.vue-->
  <div>
    <h3>Username</h3>
    <p>{{ description  }}</p>
  </div>
</template>

<style scoped>
 /*scoped wil zeggen specifiek voor component*/
</style>
