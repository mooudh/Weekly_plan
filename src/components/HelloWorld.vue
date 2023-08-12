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
            <PlanCell
              v-model="plans[day][hour][task]"
              :val="plans[day][hour]"
              @checkbox="checkbox($event, plans[day][hour], day, hour)"
            ></PlanCell>
            <!-- {{ plans[day][hour] }} -->
          </td>
        </tr>
      </tbody>
    </table>
    <button @click="FreeTime">Totla free Time</button>
    {{ totalLessonTime }}/{{ TotalTime }}
  </div>
</template>

<script setup>
import PlanCell from "./PlanCell.vue";

import { reactive, ref, onBeforeMount } from "vue";

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

const TotalTime = [[hours.length] * 2] * [days.length];
const totalLessonTime = ref(0);

const plans = reactive({
  Monday: {},
  Tuesday: {},
  Wednesday: {},
  Thursday: {},
  Friday: {},
  Saturday: {},
  Sunday: {},
});

onBeforeMount(() => {
  days.forEach((day) => {
    plans[day] = {};
    hours.forEach((hour) => {
      plans[day][hour] = { task: "", completed: false };
    });
  });
});

const checkbox = ($event, plan, day, hour) => {
  // console.log($event, plan, day, hour);
  console.log($event);
  plans[day][hour] = $event;
  console.log(plans);
};

const FreeTime = () => {
  let totalLessonTime1 = 0;

  for (const day in plans) {
    for (const hour in plans[day]) {
      if (plans[day][hour].completed) {
        totalLessonTime1 += 2;
      }
    }
  }
  totalLessonTime.value = totalLessonTime1;
  console.log(totalLessonTime);
  console.log("Total completed tasks:", totalLessonTime1);
  console.log(plans);
};
</script>

<style scoped></style>
