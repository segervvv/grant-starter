<template>
  <v-btn small class="white accent--text mb-5 mr-8" @click="onClick">
    <slot>Terug</slot>
  </v-btn>
</template>

<script>
export default {
  name: "BtnBack",
  props: {
    onClick: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped></style>
