<template>
    <div class="chat">
      <div
        v-for="(message, index) in messages"
        :key="index"
        :style="{ backgroundColor: message.color, textAlign: message.sender === 'left' ? 'left' : 'right' }"
        class="message"
      >
        <strong>{{ message.user.name.first }}:</strong> {{ message.text }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      messages: {
        type: Array,
        required: true
      }
    }
  };
  </script>
  
  <style scoped>
  .chat {
    background-color: #f4f4f4;
    padding: 1em;
    overflow-y: auto;
    height: 390px;
  }
  .message {
    padding: 0.5em;
    margin: 0.5em 0;
    border-radius: 5px;
  }
  </style>
  