<script setup>
import './style.css';
import { ref, computed, onUnmounted } from 'vue';
import ProgressBar from './components/ProgressBar.vue';

const timeInput = ref(null);
const timeLeft = ref(0);
let countdownInterval;
const totalTime = ref(0);

const formattedTime = computed(() => {
  const minutes = Math.floor(timeLeft.value / 60);
  const seconds = timeLeft.value % 60;
  return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
});

const startCountdown = () => {
  const time = parseInt(timeInput.value);

  if (isNaN(time) || time < 1 || time > 60) {
    alert("Please enter a VALID number between 1 and 60.");
    return;
  }

  clearInterval(countdownInterval);

  timeLeft.value = time;
  totalTime.value = time;

  countdownInterval = setInterval(() => {
    timeLeft.value--;

    if (timeLeft.value <= 0) {
            clearInterval(countdownInterval);
            timeLeft.value = 0;
            alert("Time's up! Let's Go!");
            return;
        }
  }, 1000);
};

onUnmounted(() => {
  clearInterval(countdownInterval);
});

</script>

<template>
  <div class="container">
    <h1>Countdown Timer</h1>
    <label for="timeInput">Please input a timer (1-60 seconds): </label>
    <input type="number" id="timeInput" v-model="timeInput" min="1" max="60" inputmode="numeric"> 

    <button @click="startCountdown">Start Countdown</button>
    <div id="timerDisplay">{{ formattedTime }}</div>

    <ProgressBar :timeLeft="timeLeft" :totalTime="totalTime" />

  </div>
</template>