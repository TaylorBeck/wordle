<template>
  <div class="flex justify-between">
    <QuestionMarkCircleIcon class="h-8 w-8 ml-3 mt-4 hover:text-green-700 hover:cursor-pointer" />
    <h1 class="font-mono font-bold text-3xl text-center my-4">
      Wayfindle
    </h1>
    <ChartBarIcon class="h-8 w-8 mr-3 mt-4 hover:text-green-700 hover:cursor-pointer" />
  </div>
  <hr class="border-t-2" />
  <div class="game flex flex-col max-w-lg mx-auto justify-evenly">
    <div class="mx-auto">
      <word
        v-for="(guess, index) in state.guesses"
        :key="index"
        :value="guess"
        :solution="state.solution"
        :submitted="index < state.currentGuessIndex"
      />
    </div>
    <keyboard
      @onKeyPress="handleKeyPressed"
      :guessedLetters="state.guessedLetters"
    />
  </div>
</template>

<script setup>
import { reactive, onMounted } from "vue";

import { QuestionMarkCircleIcon, ChartBarIcon } from "@heroicons/vue/outline";

import Word from "./components/Word.vue";
import Keyboard from "./components/Keyboard.vue";

const state = reactive({
  solution: "BOOKS",
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

        if (char == state.solution.charAt(i)) {
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

<style>
.game {
  height: 90vh;
}
</style>
