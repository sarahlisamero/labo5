<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue'; //enkel importeren wat je nodig hebt, houdt de opslag klein
    let message = ref(''); //ref is een reactieve variabele, voor simpele variabelen als int - string - boolean, reflection = iets in het oog houden
    let allMessages = reactive({
        data: ["jo", "jow", "jowkes"],
    }); //reactive is voor complexe variabelen als arrays en objecten

    //function sendMessage
    const sendMessage = () => {
        allMessages.data.push(message.value);
        message.value = ''; //message is een ref en ref heeft altijd een value nodig. dit is de value van de reflective variabele
    }
</script>

<template>
  <!--Chat.vue-->
  <div>
    <ul>
        <li v-for="m in allMessages.data">
            {{m}}
        </li>
    </ul>
    <div>
        <input v-model="message" type="text" placeholder=""> <!--zodat waarden van input en message gelijk zijn-->
        <button @click="sendMessage">Send</button> <!--@click is een eventlistener-->
    </div>
  </div>
</template>

<style scoped>
 /*scoped wil zeggen specifiek voor component*/
</style>
