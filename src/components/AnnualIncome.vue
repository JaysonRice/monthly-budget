<template>
  <v-card>
    <v-card-title class="deep-orange--text">Annual Income</v-card-title>
    <v-form @submit.prevent="saveIncome">
      <v-text-field @blur="saveIncome" outlined prefix="$" v-model="inputVal" />
    </v-form>
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
