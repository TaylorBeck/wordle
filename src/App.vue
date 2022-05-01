<template>
  <div class="flex flex-col h-screen max-w-md mx-auto justify-evenly">
    <div>
      <word v-for="(guess, index) in state.guesses" :key="index" :value="guess" :solution="state.solution" :submitted="index < state.currentGuessIndex" /> 
    </div>
    <keyboard @onKeyPress="handleKeyPressed" :guessedLetters="state.guessedLetters" />
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";

import Word from "./components/Word.vue";
import Keyboard from "./components/Keyboard.vue";

const state = reactive({
  solution: "apple",
  currentGuessIndex: 0,
  guesses: ["", "", "", "", "", ""],
  guessedLetters: {
    miss: [],
    found: [],
    hint: []
  }
});

onMounted(() => {
  window.addEventListener("keyup", (event) => {
    event.preventDefault();

    let key =
      event.keyCode === 13
        ? "{enter}"
        : event.keyCode === 8
        ? "{bksp}"
        : String.fromCharCode(event.keyCode).toUpperCase();

    handleKeyPressed(key);
  });
});

const handleKeyPressed = (key) => {
  if (state.currentGuessIndex >= 6) {
    return;
  }

  const currentGuess = state.guesses[state.currentGuessIndex];

  if (key === "{enter}") {
    if (currentGuess.length === 5) {
      state.currentGuessIndex++;

      for (let i = 0; i < currentGuess.length; i++) {
        let char = currentGuess.charAt(i);

        if (char === state.solution.charAt(i)) {
          state.guessedLetters.found.push(char);
        } else if (state.solution.indexOf(char) != -1) {
          state.guessedLetters.hint.push(char);
        } else {
          state.guessedLetters.miss.push(char);
        }
      }
    }
  } else if (key === "{bksp}") {
    state.guesses[state.currentGuessIndex] = currentGuess.slice(0, -1);
  } else if (currentGuess.length < 5) {
    const alphabetical = /[a-zA-Z]/;
    if (alphabetical.test(key)) {
      state.guesses[state.currentGuessIndex] += key;
    }
  }
};
</script>

<style></style>
