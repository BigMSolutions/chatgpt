<template>
  <q-page class="">
    <chat :messages="messages" :isLoading="isLoading" />
  </q-page>
  <q-footer>
    <q-form @submit="sendPrompt()">
      <q-toolbar class="bg-grey-3 text-black row">
        <q-input
          rounded
          outlined
          dense
          class="WAL__field col-grow q-mr-sm"
          bg-color="white"
          v-model="input"
          placeholder="Type a message"
          lazy-rules
          :rules="[
            (val) =>
              (val && val.length > 3) ||
              'Please type something over 3 chars long',
          ]"
        />
        <q-btn round flat icon="send" type="submit" />
      </q-toolbar>
    </q-form>
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
      input: "",
      messages: [],
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
      isLoading: false,
    };
  },
  methods: {
    sendPrompt() {
      if (this.input.length > 3) {
        this.messages.push({
          role: "user",
          content: this.input,
        });
        this.isLoading = true;
        this.input = "";
        var myHeaders = new Headers();
        myHeaders.append("Authorization", "Bearer " + this.token);
        myHeaders.append("Content-Type", "application/json");

        var raw = JSON.stringify({ messages: this.messages, ...this.settings });

        var requestOptions = {
          method: "POST",
          headers: myHeaders,
          body: raw,
          redirect: "follow",
        };

        fetch("https://api.openai.com/v1/chat/completions", requestOptions)
          .then(async (response) => {
            let r = JSON.parse(await response.text());
            this.messages.push(r.choices[0].message);
            this.isLoading = false;
          })
          .catch((error) => {
            this.isLoading = false;
            console.log("error", error);
          });
      } else {
      }
    },
  },
};
</script>
