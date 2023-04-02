<template>
  <div class="q-pa-md row justify-center">
    <div style="width: 100%; max-width: 400px">
      <q-chat-message
        v-for="m in messages"
        :key="m.index"
        :name="m.role"
        :text="[m.content]"
        :sent="m.role == 'user'"
      />
    </div>
  </div>
</template>
<script>
export default {
  props: ["messages"],
};
</script>
