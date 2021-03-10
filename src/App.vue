<template>
  <v-app>
    <v-main>
      <v-row>
        <v-col :cols="12" :md="8" :lg="4">
          <annual-income
            @income-change="changeIncome"
            :annualIncome="annualIncome"
          />
        </v-col>

        <v-col :cols="12" :md="8" :lg="4">
          <income-card title="Monthly Net" :netAmount="monthlyNet" />
        </v-col>
        <v-col :cols="12" :md="8" :lg="4">
          <income-card title="Annual Net" :netAmount="annualNet" />
        </v-col>
      </v-row>
      <v-row>
        <v-col :cols="12" :lg="6">
          <expenses
            @expense-submit="exspenseAdded"
            :expenses="monthlyExpenses"
          />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import AnnualIncome from "./components/AnnualIncome";
import Expenses from "./components/Expenses";
import IncomeCard from "./components/IncomeCard.vue";

export default {
  components: { AnnualIncome, Expenses, IncomeCard },
  data() {
    return {
      annualIncome: 0,
      monthlyExpenses: [],
    };
  },
  created() {
    const existingIncome = JSON.parse(localStorage.getItem("annualIncome"));
    const existingExpenses = localStorage.getItem("monthlyExpenses");
    this.annualIncome = existingIncome || 0;
    if (existingExpenses) {
      this.monthlyExpenses = JSON.parse(existingExpenses);
    }
  },
  methods: {
    changeIncome(newIncome) {
      this.annualIncome = newIncome;
      localStorage.setItem("annualIncome", JSON.stringify(newIncome));
    },
    exspenseAdded(newExpense) {
      this.monthlyExpenses.push(newExpense);
      localStorage.setItem(
        "monthlyExpenses",
        JSON.stringify(this.monthlyExpenses)
      );
    },
  },
  computed: {
    monthlyIncome() {
      return this.annualIncome / 12;
    },
    totalMonthlyExpenses() {
      return this.monthlyExpenses.reduce((total, month) => {
        return total + month.amount;
      }, 0);
    },
    annualExpenses() {
      return this.totalMonthlyExpenses * 12;
    },
    monthlyNet() {
      debugger;
      return this.monthlyIncome - this.totalMonthlyExpenses;
    },
    annualNet() {
      return this.annualIncome - this.annualExpenses;
    },
  },
};
</script>
