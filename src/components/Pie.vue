<template>
  <v-card>
    <apexchart type="pie" :options="options" :series="series"></apexchart>
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
