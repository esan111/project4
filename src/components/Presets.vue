<template>
    <div>
      <h2>Presets:</h2>
      <ul>
        <li v-for="preset in presets" :key="preset.title" @click="loadPreset(preset)">
          {{ preset.title }} ({{ preset.duration }}s)
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
  const props = defineProps(['presets']);
  const emit = defineEmits(['preset-selected']);
  
  const loadPreset = (preset) => {
    emit('preset-selected', preset); 
  };
  </script>