<template>
  <h1>Date Page</h1>
  <h2>~2025/07/05 04:18:00: {{ date1 }}</h2>
  <h2>~2025/06/19: {{ date2 }}</h2>
  <h2>~2025/06/15: {{ date3 }}</h2>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const date1 = ref("");
const date2 = ref("");
const date3 = ref("");

function formatSeconds(totalSeconds) {
  if (totalSeconds < 0) return "既成事實";

  const days = Math.floor(totalSeconds / 86400);
  const hours = Math.floor((totalSeconds % 86400) / 3600);
  const minutes = Math.floor((totalSeconds % 3600) / 60);
  const seconds = totalSeconds % 60;

  const warning = days < 5 ? " 🔴 警示" : ""; // 👈 加上警示條件
  return `${days}天 ${hours}小時 ${minutes}分鐘 ${seconds}秒${warning}`;
}

function updateDates() {
  const now = new Date();
  const t1 = Math.floor((new Date("2025/07/05 04:18:00") - now) / 1000);
  const t2 = Math.floor((new Date("2025/06/19") - now) / 1000);
  const t3 = Math.floor((new Date("2025/06/15") - now) / 1000);

  date1.value = formatSeconds(t1);
  date2.value = formatSeconds(t2);
  date3.value = formatSeconds(t3);
}

let timer;
onMounted(() => {
  updateDates();
  timer = setInterval(updateDates, 1000);
});

onUnmounted(() => {
  clearInterval(timer);
});
</script>
