<template>
  <v-card height="100%">
    <v-card-title class="deep-orange--text"
      >Monthly Expense Breakdown</v-card-title
    >

    <apexchart
      type="pie"
      :options="options"
      :series="series"
      height="300"
    ></apexchart>
  </v-card>
</template>

<script>
export default {
  props: ["expenses", "totalAmount"],
  computed: {
    series() {
      return this.expenses.map((e) => e.amount);
    },
    options() {
      return { labels: this.expenses.map((e) => e.name) };
    },
  },
};
</script>

<style></style>
