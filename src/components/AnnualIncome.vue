<template>
  <v-card>
    <v-card-title>Annual Income</v-card-title>
    <v-text-field outlined prefix="$" v-model="inputVal" />
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
};
</script>

<style></style>
