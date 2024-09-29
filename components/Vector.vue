<template>
    <div :class="classes">
      <img :src="imageSrc" :alt="altText" />
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    imageSrc: {
      type: String,
      default: '/assets/vector-auth.svg', // مسیر پیش‌فرض به SVG
    },
    altText: {
      type: String,
      default: '', // متن پیش‌فرض alt
    },
    classes: {
      type: String,
      default: '', // کلاس‌های اضافی
    },
  });
  </script>  