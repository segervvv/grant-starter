<template>
  <ValidationProvider :name="$attrs.label" :rules="rules" v-slot="{ errors }">
    <v-radio-group
      v-model="innerValue"
      :error-messages="errors"
      v-bind="$attrs"
      v-on="$listeners"
    >
      <div>
        <v-radio value="ke1" color="textStat">
          <template v-slot:label> {{ optionA }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 1">
        <v-radio value="ke2" color="textStat">
          <template v-slot:label> {{ optionB }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 2">
        <v-radio value="ke3" color="textStat">
          <template v-slot:label>{{ optionC }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 3">
        <v-radio value="ke4" color="textStat">
          <template v-slot:label>{{ optionD }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 4">
        <v-radio value="ke5" color="textStat">
          <template v-slot:label>{{ optionE }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 5">
        <v-radio value="ke6" color="textStat">
          <template v-slot:label>{{ optionF }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 6">
        <v-radio value="ke7" color="textStat">
          <template v-slot:label>{{ optionG }} </template>
        </v-radio>
      </div>
      <div class="mt-3" v-if="nrOptions > 7">
        <v-radio value="ke8" color="textStat">
          <template v-slot:label>{{ optionH }} </template>
        </v-radio>
      </div>
    </v-radio-group>
  </ValidationProvider>
</template>

<script>
export default {
  name: "BaseRadio",
  components: {},
  props: {
    rules: {
      type: [Object, String],
      default: "",
    },
    value: {
      type: String,
      default: null,
    },
    nrOptions: {
      default: 2,
    },
    optionA: {
      type: String,
      default: null,
    },
    optionB: {
      type: String,
      default: null,
    },
    optionC: {
      type: String,
      default: null,
    },
    optionD: {
      type: String,
      default: null,
    },
    optionE: {
      type: String,
      default: null,
    },
    optionF: {
      type: String,
      default: null,
    },
    optionG: {
      type: String,
      default: null,
    },
    optionH: {
      type: String,
      default: null,
    },
  },
  data: () => ({
    innerValue: "",
  }),
  watch: {
    // Handles internal model changes.
    innerValue(newVal) {
      this.$emit("input", newVal);
    },
    // Handles external model changes.
    value(newVal) {
      this.innerValue = newVal;
    },
  },
  created() {
    if (this.value) {
      this.innerValue = this.value;
    }
  },
};
</script>
