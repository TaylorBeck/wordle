<template>
  <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
    <keyboard @onKeyPress="handleKeyPressed" />
  </div>
</template>

<script setup>
import { onMounted } from "vue";

import Keyboard from "./components/Keyboard.vue";

onMounted(() => {
  window.addEventListener("keyup", (event) => {
    event.preventDefault();

    let key =
      event.keyCode == 13
        ? "{enter}"
        : event.keyCode == 8
        ? "{bksp}"
        : String.fromCharCode(event.keyCode).toUpperCase();

    handleKeyPressed(key);
  });
});

const handleKeyPressed = (key) => {
  console.log(key);
};
</script>


<style></style>
