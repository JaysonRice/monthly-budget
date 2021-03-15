<template>
  <v-app>
    <v-main class="pa-3 green lighten-3">
      <v-row justify="center">
        <v-col :cols="12" :md="8" :lg="4">
          <annual-income
            @income-change="changeIncome"
            :annualIncome="annualIncome"
          />
        </v-col>

        <v-col :cols="12" :md="6" :lg="4">
          <income-card title="Monthly Net" :netAmount="monthlyNet" />
        </v-col>
        <v-col :cols="12" :md="6" :lg="4">
          <income-card title="Annual Net" :netAmount="annualNet" />
        </v-col>
      </v-row>
      <v-row>
        <v-col :cols="12" :md="6">
          <expenses
            @expense-submit="exspenseAdded"
            @expense-delete="exspenseDeleted"
            :expenses="monthlyExpenses"
          />
        </v-col>
        <v-col :cols="12" :md="6">
          <pie :expenses="monthlyExpenses" :totalAmount="annualExpenses" />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import AnnualIncome from "./components/AnnualIncome";
import Expenses from "./components/Expenses";
import IncomeCard from "./components/IncomeCard";
import Pie from "./components/Pie";

export default {
  components: { AnnualIncome, Expenses, IncomeCard, Pie },
  data() {
    return {
      annualIncome: 0,
      monthlyExpenses: [],
    };
  },
  created() {
    const existingAnnual = localStorage.getItem("annualIncome");

    if (existingAnnual) {
      this.annualIncome = parseFloat(existingAnnual);
    }

    const existingExpenses = localStorage.getItem("monthlyExpenses");
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
    exspenseDeleted(expenseToDelete) {
      // Filter the deleted expense out of the array before setting local storage again
      this.monthlyExpenses = this.monthlyExpenses.filter((e) => {
        return e !== expenseToDelete;
      });
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
      return (this.monthlyIncome - this.totalMonthlyExpenses).toFixed(2);
    },
    annualNet() {
      return (this.annualIncome - this.annualExpenses).toFixed(2);
    },
  },
};
</script>
