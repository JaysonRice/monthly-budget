<template>
  <v-card>
    <v-card-title class="deep-orange--text"> Monthly Expenses</v-card-title>
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
      this.$emit("expense-submit", { name: this.name, amount: this.amount });
      this.name = "";
      this.amount = null;
    },
    saveExpenses() {},
  },
};
</script>

<style></style>
