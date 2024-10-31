<template>
    <div class="user">
      <img :src="user.picture.large" />
      <p>{{ user.name.first }} {{ user.name.last }}</p>
      <input v-model="newColor" type="color">
      <textarea v-model="newMessage" placeholder="Escribe un mensaje..."></textarea>
      <button @click="sendMessage">Enviar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      user: {
        type: Object,
        required: true
      },
      color: {
        type: String,
        required: true
      }
    },
    data() {
      return {
        newMessage: "",
        newColor: this.color
      };
    },
    methods: {
      sendMessage() {
        if (this.newMessage.trim()) {
          this.$emit("sendMessage", {
            user: this.user,
            text: this.newMessage,
            color: this.newColor
          });
          this.newMessage = "";
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .user {
    text-align: center;
    margin: 10px;
  }
  textarea {
    width: 98%;
    height: 100px;
    margin-top: 5px;
    border-radius: 5px;
  }
  button {
    margin-top: 5px;
    padding: 5px 10px;
  }
  img {
    width: 180px;
    height: 180px;
  }
  input {
    width: 100%;
  }
  button {
    width: 100%;
  }
  </style>
  