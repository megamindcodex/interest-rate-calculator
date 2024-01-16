<template>
  <div class="div">
    <label>
      percent:
      <input type="number" v-model="percentage" />
    </label>
    <label>
      amount
      <input type="number" v-model="principal" />
    </label>
    <label>
      nFDays
      <input type="number" v-model="numberOfDays" />
    </label>
    <span>Daily Interest: {{ dailyInterest }}</span>
    <span>total interest: {{ totalInterest }}</span>
    <span>overallTotal: {{ overallTotal }}</span>
    <!-- <button @click="calculate">cal</button> -->
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue';

const percentage = ref();
const principal = ref();
const numberOfDays = ref();
const dailyInterest = ref(0);
const totalInterest = ref(0);
const overallTotal = ref(0);

const calDailyInterest = () => {
  if (percentage.value !== undefined && principal.value !== undefined) {
    dailyInterest.value = (percentage.value * principal.value) / 100;
  }
};

const calTotalInterest = () => {
  if (dailyInterest.value !== undefined && numberOfDays !== undefined) {
    totalInterest.value = dailyInterest.value * numberOfDays.value;
  }
};

const calOverall = () => {
  overallTotal.value = principal.value + totalInterest.value;
};

watchEffect(() => {
  calDailyInterest();
  calTotalInterest();
  calOverall();
});

watchEffect(() => {});
</script>

<style scoped>
.div {
  display: flex;
  flex-direction: column;
}
</style>
