<template>
  <div class="keyboard"></div>
</template>

<script setup>
import Keyboard from 'simple-keyboard';
import 'simple-keyboard/build/css/index.css';

import { ref, onMounted } from 'vue';

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
    onKeyPress: onKeyPress
  })
});
</script>

<style></style>