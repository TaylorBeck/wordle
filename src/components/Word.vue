<template>
  <div class="grid max-w-xs grid-cols-5 gap-4 mb-2 last:mb-0">
    <letter 
      v-for="n in 5"
      :key="n"
      :letter="value[n - 1]"
      :color="colors[n - 1]"
    />
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

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

const colors = ref(["", "", "", "", "", ""]);

watch(
  () => props.submitted,
  async (submitted, prevSubmitted) => {
    if (props.submitted) {
      let solution = props.solution;
      let guess = props.value;

      let temp = ["gray", "gray", "gray", "gray", "gray"];
      let letterPool = [];
      for (let i = 0; i < 5; i++) {
        if (guess.charAt(i) === solution.charAt(i)) {
          temp[i] = "green";
        } else {
          letterPool.push(solution.charAt(i));
        }
      }

      for (let i = 0; i < 5; i++) {
        if (temp[i] === "gray") {
          if (letterPool.indexOf(guess.charAt(i)) != -1) {
            letterPool.splice(letterPool.indexOf(guess.charAt(i)), 1);
            temp[i] = "yellow";
          }
        }

        colors.value[i] = temp[i];
        await new Promise((resolve) => setTimeout(resolve, 650));
      }
    }
  }
);
</script>

<style>
</style>