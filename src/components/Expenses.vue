<template>
  <v-card>
    <v-card-title class="deep-orange--text"> Monthly Expenses</v-card-title>
    <v-card-text>
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
              <td>{{ expense.amount }}</td>
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

      <v-card-subtitle> Monthly Expenses</v-card-subtitle>

      <v-form @submit.prevent="handleSubmit">
        <v-row>
          <v-col :sm="5">
            <v-text-field outlined label="Expense Name" v-model="name" />
          </v-col>
          <v-col :sm="5">
            <v-text-field outlined label="Amount" prefix="$" v-model="amount" />
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
    };
  },
  methods: {
    handleSubmit() {
      this.$emit("expense-submit", { name: this.name, amount: +this.amount });
      this.name = "";
      this.amount = null;
    },
    handleRemove(expense) {
      this.$emit("expense-delete", expense);
    },
  },
};
</script>

<style></style>
