<template>
  <v-card>
    <v-card-title class="deep-orange--text"> Monthly Expenses</v-card-title>
    <v-card-text class="expensesContainer">
      <v-simple-table :height="200">
        <template v-slot:default>
          <thead>
            <tr>
              <th>Expense</th>
              <th>Amount</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="expense in expenses" :key="expense.name">
              <td>{{ expense.name }}</td>
              <td>${{ expense.amount }}</td>
              <td class="text-right">
                <v-btn
                  icon
                  large
                  color="deep-orange"
                  dark
                  @click="handleRemove(expense)"
                >
                  <v-icon>mdi-minus-circle-outline</v-icon>
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <v-divider></v-divider>

      <v-card-subtitle> Add Expense</v-card-subtitle>

      <v-form @submit.prevent="handleSubmit" ref="expenseForm">
        <v-row>
          <v-col :sm="5">
            <v-text-field
              color="deep-orange"
              outlined
              label="Expense Name"
              v-model="name"
              :rules="validators.name"
              dense
            />
          </v-col>
          <v-col :sm="5">
            <v-text-field
              color="deep-orange"
              outlined
              type="number"
              label="Amount"
              prefix="$"
              v-model="amount"
              onkeydown="return event.keyCode !== 69"
              :rules="validators.amount"
              dense
            />
          </v-col>
          <v-col :sm="2">
            <v-btn icon large color="deep-orange" dark type="submit">
              <v-icon>mdi-plus-circle-outline</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["expenses"],
  data() {
    return {
      name: "",
      amount: null,
      validators: {
        name: [(val) => !!val || "Name of expense is required"],
        amount: [
          (val) => !!val || "Expense must have an amount",
          (val) => val > 0 || "Expense must not be negative",
        ],
      },
    };
  },
  methods: {
    handleSubmit() {
      const isValid = this.$refs.expenseForm.validate();
      if (!isValid) {
        // Form is not valid. Exit the method
        return;
      }
      this.$emit("expense-submit", {
        name: this.name,
        amount: +this.amount,
      });
      this.name = "";
      this.amount = null;
      this.$refs.expenseForm.resetValidation();
    },
    handleRemove(expense) {
      this.$emit("expense-delete", expense);
    },
  },
};
</script>

<style>
.expensesContainer {
  padding-bottom: 0.8em;
}
</style>
