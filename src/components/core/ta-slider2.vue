<template>
  <div class="mt-3">
    <div><br /><br /></div>
    <v-slider
      prop="value"
      v-model="joho"
      :value="value"
      :color="color"
      always-dirty
      min="-100"
      max="100"
      step="5"
      thumb-label="always"
      :thumb-color="color"
      :track-color="color"
    >
      <template v-slot:append>
        <v-icon color="secondary">mdi-plus-circle-outline</v-icon>
      </template>
      <template v-slot:prepend>
        <v-icon color="accent">mdi-minus-circle-outline</v-icon>
      </template>
    </v-slider>

    <v-row class="mt-0 mb-2">
      <v-col :cols="4"
        ><div class="caption accent--text text-left">
          Helemaal mee oneens
        </div></v-col
      >
      <v-col :cols="4"></v-col>
      <v-col :cols="4"
        ><div class="caption secondary--text text-right">
          Helemaal mee eens
        </div></v-col
      >
    </v-row>
  </div>
</template>

<script>
export default {
  name: "ta-slider2",
  props: {
    value: null,
  },
  data() {
    return {};
  },

  computed: {
    joho: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit("input", val);
      },
    },

    color() {
      if (this.value < 0) return "accent";
      if (this.value > 0) return "secondary";
      return "#cbc4bc";
    },
  },
};
</script>

<style scoped></style>
