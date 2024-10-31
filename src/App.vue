<template>
  <div id="app" class="chat-container">
    <UserMsg v-if="user1" :user="user1" @sendMessage="addMessage" color="lightblue" />
    <ChatMsg :messages="messages" />
    <UserMsg v-if="user2" :user="user2" @sendMessage="addMessage" color="lightpink" />
  </div>
</template>

<script>
import axios from "axios";
import ChatMsg from "./components/ChatMsg.vue";
import UserMsg from "./components/UserMsg.vue";

export default {
  components: { ChatMsg, UserMsg },
  data() {
    return {
      user1: null,
      user2: null,
      messages: []
    };
  },
  methods: {
    async fetchUsers() {
      const ruta = "https://randomuser.me/api/?results=2";
      try {
        const response = await axios.get(ruta);
        this.user1 = response.data.results[0];
        this.user2 = response.data.results[1];
      } catch (error) {
        alert("Error cargando usuarios en ruta: . . . " + ruta);
      }
    },
    addMessage(message) {
      this.messages.push({
        ...message,
        sender: message.user === this.user1 ? 'left' : 'right'
      });
      console.log(message);
    }
  },
  created() {
    this.fetchUsers();
  }
};
</script>

<style scoped>
.chat-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 80%;
  margin: 0 auto;
  padding: 20px;
  gap: 20px;
}

.chat-container > * {
  flex: 1;
  max-width: 370px;
}

.chat-container .chat-msg {
  flex: 2;
  border: 1px solid #ccc;
  border-radius: 10px;
  background-color: #f4f4f4;
  padding: 10px;
  overflow-y: auto;
  height: 400px;
}

.user-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 10px;
  background-color: #fff;
}

.user-container img {
  border-radius: 50%;
  width: 100px;
  height: 100px;
}

.user-container p {
  font-weight: bold;
  margin-top: 10px;
}

textarea {
  width: 100%;
  height: 50px;
  margin-top: 10px;
  resize: none;
}

button {
  margin-top: 5px;
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
