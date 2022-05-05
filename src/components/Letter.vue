<template>
  <div class="col-span-1 flex items-center justify-center h-14 w-14 border-2 border-gray-300 uppercase rounded-md font-mono font-extrabold text-2xl">
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