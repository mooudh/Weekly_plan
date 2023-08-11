<template>
  <div>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Time</th>
          <th v-for="day in days" :key="day">{{ day }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="hour in hours" :key="hour">
          <td>{{ hour }}</td>
          <td v-for="day in days" :key="day">
            <input type="text" v-model="plans[day][hour]" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const days = reactive([
  "Saturday",
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
]);

const hours = reactive([
  "8:00",

  "10:00",
  "12:00",
  "14:00",
  "16:00",
  "18:00",
  "20:00",
  "22:00",
]);

const plans = reactive({
  Monday: {},
  Tuesday: {},
  Wednesday: {},
  Thursday: {},
  Friday: {},
  Saturday: {},
  Sunday: {},
});
</script>

<style lang="scss" scoped></style>
