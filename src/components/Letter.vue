<template>
  <div class="col-span-1 flex items-center justify-center h-16 border-2 border-gray-300 uppercase rounded-md">
    {{ letter }}
  </div>
</template>

<script setup>
 const props = defineProps({
   letter: {
     type: String,
     required: false,
     default: ""
   }
 });
</script>

<style></style>