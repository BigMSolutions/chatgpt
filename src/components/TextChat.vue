<template>
  <div class="q-pa-md row justify-center">
    <div style="width: 100%">
      <q-chat-message
        v-for="m in messages"
        :key="m.index"
        :name="m.role"
        :text="[m.content]"
        :sent="m.role == 'user'"
      />
      <q-chat-message v-if="isLoading">
        <template v-slot:name>assistant</template>
        <q-spinner-dots size="2rem" />
      </q-chat-message>
    </div>
  </div>
</template>
<script>
export default {
  props: ["messages", "isLoading"],
};
</script>
