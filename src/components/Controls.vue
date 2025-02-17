<template>
    <div>
        <button @click="start">Start</button>
        <button @click="stop">Stop</button>
        <button @click="reset">Reset</button>
        <button @click="resume" v-if="paused">Resume</button>
    </div>
</template>

<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits (['start', 'stop', 'reset', 'resume']);

const start = () => emit('start');
const stop = () => emit('stop');
const reset = () => emit('reset');
const resume = () => emit('resume');
</script>