<template>
  <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
    <div>
      <word v-for="(guess, index) in state.guesses" :key="index" :value="guess" :solution="state.solution" :submitted="i < state.currentGuessIndex" /> 
    </div>
    <keyboard @onKeyPress="handleKeyPressed" />
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";

import Word from "./components/Word.vue";
import Keyboard from "./components/Keyboard.vue";

const state = reactive({
  solution: "apple",
  guesses: ["", "", "", "", "", ""],
  currentGuessIndex: 0 
});

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
