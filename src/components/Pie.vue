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
      return {
        labels: this.expenses.map((e) => e.name),
        colors: [
          "#FF8A65",
          "#FDD835",
          "#81C784",
          "#F4511E",
          "#FFF176",
          "#43A047",
          "#BF360C",
          "#2E7D32",
          "#F9A825",
        ],
        // theme: {
        //   palette: "palette10",
        //   monochrome: {
        //     enabled: true,
        //     color: "#FDD835",
        //   },
        // },
      };
    },
  },
};
</script>

<style></style>
