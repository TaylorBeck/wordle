<template>
  <div class="grid max-w-xs grid-cols-5 gap-4 mb-2 last:mb-0">
    <letter v-for="n in 5" :key="n" :letter="value[n - 1]" />
  </div>
</template>

<script setup>
import Letter from "./Letter.vue";

const props = defineProps({
  value: {
    type: String,
    required: true
  },
  solution: {
    type: String,
    required: true
  },
  submitted: {
    type: Boolean,
    required: true
  }
});
</script>

<style>
</style>