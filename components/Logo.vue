<template>
    <div :class="classes">
      <img :src="imageSrc" :alt="altText" />
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    classes: {
      type: String,
      default: 'overflow-hidden rounded-lg w-[45px]',
    },
    imageSrc: {
      type: String,
      default: '/Logo.png',
    },
    altText: {
      type: String,
      default: 'Timeman',
    },
  });
  </script>
  
  <style scoped>
  </style>
  