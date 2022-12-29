<template>
  <div class="keyboard"></div>
</template>

<script setup>
import Keyboard from 'simple-keyboard';
import 'simple-keyboard/build/css/index.css';

import { ref, onMounted, watch } from 'vue';

const props = defineProps({
  guessedLetters: {
    type: Object,
    required: true
  }
});

const emit = defineEmits([
  'onKeyPress'
]);

const keyboard = ref(null);

const onKeyPress = (key) => {
  emit('onKeyPress', key);
};

onMounted(() => {
  keyboard.value = new Keyboard('keyboard', {
    layout: {
      default: [
        'Q W E R T Y U I O P {bksp}',
        'A S D F G H J K L {enter}',
        'Z X C V B N M'
      ]
    },
    buttonTheme: [
      {
        class: 'hg-green',
        buttons: '{enter}'
      },
      {
        class: 'hg-black',
        buttons: '{bksp}'
      }
    ],
    display: {
      '{enter}': 'ENTER',
      '{bksp}': " ← "
    },
    theme: "hg-theme-default bg-transparent",
    onKeyPress: onKeyPress
  })
});

watch(
  () => props.guessedLetters,
  (guessedLetters, prevGuessedLetters) => {
    keyboard.value.addButtonTheme(
      guessedLetters.miss.join(" "), 
      "miss"
    );
    keyboard.value.addButtonTheme(
      guessedLetters.found.join(" "), 
      "found"
    );
    keyboard.value.addButtonTheme(
      guessedLetters.hint.join(" "), 
      "hint"
    );
  },
  { deep: true }
);
</script>

<style>
.miss {
  @apply bg-gray-400 !important;
  @apply text-white;
}
.found {
  @apply bg-green-600 !important;
  @apply text-white;
}
.hint:not(.found) {
  @apply bg-yellow-400 !important;
  @apply text-white;
}
</style>