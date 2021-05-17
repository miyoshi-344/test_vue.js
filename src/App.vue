<template>
  <div id="app">
    <input type="text" name="text" v-model="newText" />
    <button @click="sendText">送信</button>
    <div v-for="item in textLists" :key="item.id">
      <p>{{item.text}}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      newText: "",
      textLists: [],
    };
  },
  methods: {
    async getText() {
      const resData = await axios.get("http://127.0.0.1:8000/api/");
      this.textLists = resData.data.data;
    },
    async sendText() {
      const sendData = {
        text: this.newText,
      };
      await axios.post("http://127.0.0.1:8000/api/", sendData);
      await this.getText();
    }
  }
};
</script>