<template>
    <div class="progress-bar" :style="{ width: progressPercent + '%' }"></div>
  </template>
  
  <script setup>
  import { computed } from 'vue';
  
  const props = defineProps(['timeLeft', 'totalTime']);
  
  const progressPercent = computed(() => {
    return (props.timeLeft / props.totalTime) * 100;
  });
  </script>
  