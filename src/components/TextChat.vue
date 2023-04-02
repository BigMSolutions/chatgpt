<template>
  <div class="q-pa-md row justify-center">
    <div style="width: 100%; max-width: 400px">
      <q-chat-message
        v-for="m in messages"
        :key="m.index"
        :name="m.sender"
        :text="[m.message]"
        :sent="m.sender != 'chatgpt'"
      />
    </div>
  </div>
</template>
<script>
export default {
  props: ["messages"],
};
</script>
