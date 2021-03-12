<template>
  <v-card height="100%">
    <v-card-title class="deep-orange--text">{{ title }}</v-card-title>

    <v-card-text>
      <h1 class="net-amount pb-5" :class="netStatus">${{ displayAmount }}</h1>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["title", "netAmount"],
  computed: {
    displayAmount() {
      return new Intl.NumberFormat().format(this.netAmount);
    },
    netStatus() {
      return this.netAmount >= 0 ? "green--text" : "red--text";
    },
  },
};
</script>

<style>
.net-amount {
  font-size: 4em;
  margin-top: 20px;
  text-align: center;
}
</style>
