<script setup>
import './style.css';
import { ref, computed, onUnmounted } from 'vue';
import ProgressBar from './components/ProgressBar.vue';
import Controls from './components/Controls.vue';
import Presets from './components/Presets.vue';

const timeInput = ref(null);
const timeLeft = ref(0);
let countdownInterval;
const totalTime = ref(0);
const alertMessage = ref(null);

const presets = ref([
  { title: 'Quick Break', duration: 5 },
  { title: 'Focus Time', duration: 25 },
]);

const formattedTime = computed(() => {
  const minutes = Math.floor(timeLeft.value / 60);
  const seconds = timeLeft.value % 60;
  return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
});

const startCountdown = () => {
  const time = parseInt(timeInput.value);

  if (isNaN(time) || time < 1 || time > 60) {
    alertMessage.value = "Please enter a VALID number between 1 and 60.";
    timeInput.value
    return;
  }

  clearInterval(countdownInterval);
  timeLeft.value = time;
  totalTime.value = time;
  alertMessage.value = null;

  countdownInterval = setInterval(() => {
    timeLeft.value--;

    if (timeLeft.value <= 0) {
            clearInterval(countdownInterval);
            timeLeft.value = 0;
            alertMessage.value = "Time's up! Let's Go!";
            setTimeout(() => alert("Time's up! Let's Go!"), 0);
            return;
        }
  }, 1000);
};

const stopCountdown = () => {  
  clearInterval(countdownInterval);
};

const resetCountdown = () => { 
  clearInterval(countdownInterval);
  timeLeft.value = 0;
  totalTime.value = 0;
  alertMessage.value = null; 
  timeInput.value = null;   
};

const loadPreset = (preset) => {  
  timeInput.value = preset.duration;
  startCountdown();
};



onUnmounted(() => {
  clearInterval(countdownInterval);
});

</script>

<template>
    <div class="container">
      <h1>Countdown Timer</h1>

    <Presets :presets="presets" @preset-selected="loadPreset" /> <label for="timeInput">Or enter time (1-60 seconds):</label>
    <input type="number" id="timeInput" v-model="timeInput" min="1" max="60" inputmode="numeric"> 

    <Controls class="controls" @start="startCountdown" @stop="stopCountdown" @reset="resetCountdown" /> <div id="timerDisplay">{{ formattedTime }}</div>

    <ProgressBar :timeLeft="timeLeft" :totalTime="totalTime" />

  </div>
</template>