<template>
  <h1>
    ~{{ slug }}: {{ timeDiff.days }}天 {{ timeDiff.hours }}小時
    {{ timeDiff.minutes }}分鐘 {{ timeDiff.seconds }}秒
    <span v-if="timeDiff.totalMs > 0 && timeDiff.totalMs < warningThresholdMs"
      >🔴 警示</span
    >
  </h1>

  <h2>
    <span v-if="timeDiff.totalMs === 0">就是現在！</span>
  </h2>
</template>

<script setup>
import { useRoute } from "vue-router";
import { ref, onMounted, onUnmounted } from "vue";

const route = useRoute();
const slug = ref("");

const timeDiff = ref({
  isPast: true,
  totalMs: 0,
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

// 預警閾值（毫秒）→ 5 天內為紅色警示
const warningThresholdMs = 5 * 24 * 60 * 60 * 1000;

const param = route.params.slug;

// 轉成 "YYYY-MM-DD"
if (param && param.length === 8) {
  slug.value = `${param.slice(0, 4)}/${param.slice(4, 6)}/${param.slice(6, 8)}`;
} else {
  slug.value = param || "";
}

function updateTimeDiff() {
  const now = new Date();
  const target = new Date(slug.value);
  const diffMs = now.getTime() - target.getTime();
  const totalMs = Math.abs(diffMs);

  timeDiff.value = {
    isPast: diffMs > 0,
    totalMs,
    days: Math.floor(totalMs / (1000 * 60 * 60 * 24)),
    hours: Math.floor((totalMs % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)),
    minutes: Math.floor((totalMs % (1000 * 60 * 60)) / (1000 * 60)),
    seconds: Math.floor((totalMs % (1000 * 60)) / 1000),
  };
}

let intervalId = null;

onMounted(() => {
  updateTimeDiff();
  intervalId = setInterval(updateTimeDiff, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>
