<template>
  <v-app>
    <v-main>
      <v-row>
        <v-col :cols="12" :md="8" :lg="4">
          <annual-income :annualIncome="annualIncome" />
        </v-col>
        <v-col :cols="12" :md="8" :lg="4">
          <expenses @expense-submit="addExpense" :expenses="monthlyExpenses" />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import AnnualIncome from "./components/AnnualIncome";
import Expenses from "./components/Expenses";

export default {
  components: { AnnualIncome, Expenses },
  data() {
    return {
      annualIncome: 0,
      monthlyExpenses: [],
    };
  },
};
</script>
