<template>
  <q-page class="row">
    <chat :messages="messages" />
  </q-page>
  <q-footer elevated class="bg-grey-8 text-white">
    <div class="row">
      <q-input outlined v-model="text" label="Outlined" />
      <q-btn color="primary" icon="mail" label="On Left" />
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
      messages: [
        {
          sender: "me",
          message: "test 1",
        },
        {
          sender: "chatgpt",
          message: "respense one",
        },
      ],
    };
  },
};
</script>
