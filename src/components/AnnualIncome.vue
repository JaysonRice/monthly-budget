<template>
  <v-card height="100%">
    <v-card-title class="deep-orange--text">Annual Income</v-card-title>
    <v-card-text>
      <v-form @submit.prevent="saveIncome">
        <v-text-field
          color="deep-orange"
          @blur="saveIncome"
          outlined
          prefix="$"
          v-model="inputVal"
        />
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["annualIncome"],
  data() {
    return {
      inputVal: +this.annualIncome,
    };
  },
  methods: {
    saveIncome() {
      this.$emit("income-change", +this.inputVal);
    },
  },
};
</script>

<style></style>
