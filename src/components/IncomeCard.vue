<template>
  <v-card>
    <v-card-title class="deep-orange--text">{{ title }}</v-card-title>
    <v-card-text>
      <v-card-text>
        <h1 :class="netStatus">{{ displayAmount }}</h1>
      </v-card-text>
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

<style></style>
