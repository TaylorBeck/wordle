<template>
  <div class="keyboard"></div>
</template>

<script setup>
import Keyboard from "simple-keyboard";
import "simple-keyboard/build/css/index.css";

import { ref, onMounted } from "vue";

const emit = defineEmits([
  "onKeyPress"
]);

const keyboard = ref(null);

const onKeyPress = (key) => {
  emit("onKeyPress", key);
};

onMounted(() => {
  keyboard.value = new Keyboard("keyboard", {
    layout: {
      default: [
        "q w e r t y u i o p {bksp}",
        "a s d f g h j k l {enter}",
        "z x c v b n m"
      ]
    },
    buttonTheme: [
      {
        class: "hg-green",
        buttons: "{enter}"
      },
      {
        class: "hg-black",
        buttons: "{bksp}"
      }
    ],
    onKeyPress: onKeyPress
  })
});
</script>

<style>
</style>