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
  
  <style scoped>
  .progress-bar {
    height: 10px;
    background-color: lightgreen;
    width: 0%;
    transition: width 0.3s linear;
    margin-top: 10px;
  }
  </style>