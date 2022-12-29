<template>
  <div 
    class="col-span-1 flex items-center justify-center h-14 w-14 border-2 border-gray-300 uppercase rounded-md font-mono font-extrabold text-2xl transition-all duration-300"
    :class="{
      'border-gray-500 bg-gray-500 text-white' : color === 'gray',
      'border-green-600 bg-green-600 text-white' : color === 'green',
      'border-yellow-500 bg-yellow-500 text-white' : color === 'yellow'
    }"
  >
    {{ letter }}
  </div>
</template>

<script setup>
const props = defineProps({
  letter: {
    type: String,
    required: false,
    default: ""
  },
  color: {
    type: String,
    required: false,
    default: ""
  }
});
</script>

<style></style>