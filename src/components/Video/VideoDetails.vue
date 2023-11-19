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
  h3{
      font-size: 24px;
      font-family: sans-serif;
      color: palevioletred;
  }
  p{
      font-size: 18px;
      font-family: sans-serif;
  }
  div{
      background-color: #f5f5f5;
      width: 40%;
  }
</style>
