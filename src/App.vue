<template>
  <div
    :class="`min-h-screen flex flex-col transition-colors duration-300 ${
      isDarkMode ? 'bg-gray-900 text-white' : 'bg-white text-gray-900'
    }`"
  >
    <Header :isDarkMode="isDarkMode" @toggleDarkMode="toggleDarkMode" />
    <Countdown />
     <p class="text-base text-sm text-gray-500 text-center">Made with &#x2764;&#xfe0f;, by Vitor Ferronato</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import Countdown from "./components/Countdown.vue";

const isDarkMode = ref(true);

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
};
</script>
