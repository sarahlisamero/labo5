<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue'; //enkel importeren wat je nodig hebt, houdt de opslag klein
    let message = ref(''); //ref is een reactieve variabele, voor simpele variabelen als int - string - boolean, reflection = iets in het oog houden
    let allMessages = reactive({
        data: [],
    }); //reactive is voor complexe variabelen als arrays en objecten

    onMounted(async () => {
    try {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data;
    } catch (error) {
        console.error(error);
    }
    });

    const sendMessage = async () => {
    try {
      const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ text: message.value, user: 'Sarah-Lisa'}),
      });

      if (response.ok) {
        // update message als het succesvol verzonden is
        const data = await response.json();
        const newMessage = { id: data.id, text: message.value, user: 'Sarah-Lisa'};
        allMessages.data.push(newMessage);
        message.value = ''; // leeg input veld na send
      } else {
        console.error('Failed to send message');
      }
    } catch (error) {
      console.error(error);
    }
  };
</script>

<template>
  <!--Chat.vue-->
  <div>
    <ul>
        <li v-for="m in allMessages.data.slice(-15).reverse()" :key="m.id">
          <div class="user">{{ m.user }}:</div> 
          <div class="message">{{ m.text }}</div>
      </li>
    </ul>
    <div class="textbox">
        <input v-model="message" type="text" placeholder=""> <!--zodat waarden van input en message gelijk zijn-->
        <button @click="sendMessage">Send</button> <!--@click is een eventlistener-->
    </div>
  </div>
</template>

<style scoped>
 /*scoped wil zeggen specifiek voor component*/
  ul{
      list-style-type: none;
      padding: 0;
  }
  li{
      margin-bottom: 10px;
  }
  .user{
      font-weight: bold;
      font-size: 20px;
      font-family: sans-serif;
  }
  .message{
      font-size: 18px;
      font-family: sans-serif;
  }
  .textbox input, .textbox button{
      padding: 10px;
  }
  .textbox button{
      background-color: palevioletred;
      border: none;
      color: white;
      font-size: 16px;
      cursor: pointer;
  }
</style>
