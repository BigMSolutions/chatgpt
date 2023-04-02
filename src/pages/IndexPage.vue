<template>
  <q-page class="">
    <chat :messages="messages" />
  </q-page>
  <q-footer elevated class="bg-white text-black">
    <div class="row">
      <q-input outlined v-model="text" label="Outlined" />
      <q-btn color="primary" icon="send" flat />
    </div>
  </q-footer>
</template>

<script>
import chat from "../components/TextChat.vue";
export default {
  components: {
    chat,
  },
  data() {
    return {
      sender: "mossaab",
      messages: [
        {
          role: "user",
          content: "Who won the world series in 2020?",
        },
        {
          role: "assistant",
          content: "The Los Angeles Dodgers won the World Series in 2020.",
        },
        {
          role: "user",
          content: "Where was it played?",
        },
      ],
      settings: {
        model: "gpt-3.5-turbo",
        temperature: 1,
        top_p: 1,
        n: 1,
        stream: false,
        max_tokens: 250,
        presence_penalty: 0,
        frequency_penalty: 0,
      },
      token: "",
    };
  },
  methods: {
    sendPrompt() {
      var myHeaders = new Headers();
      myHeaders.append("Authorization", "Bearer " + this.token);
      myHeaders.append("Content-Type", "application/json");

      var raw = JSON.stringify({ messages, ...settings });

      var requestOptions = {
        method: "POST",
        headers: myHeaders,
        body: raw,
        redirect: "follow",
      };

      fetch("https://api.openai.com/v1/chat/completions", requestOptions)
        .then((response) => response.text())
        .then((result) => console.log(result))
        .catch((error) => console.log("error", error));
    },
  },
};
</script>
