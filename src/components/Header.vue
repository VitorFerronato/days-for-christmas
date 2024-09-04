<template>
  <header
    :class="`w-full py-4 text-center flex justify-end  items-center px-4 ${
      isDarkMode ? 'bg-gray-800 text-white' : 'bg-gray-200 text-gray-900'
    }`"
  >
    <button @click="toggleDarkMode" class="text-2xl focus:outline-none">
      <span v-if="isDarkMode">🌞</span>
      <span v-else>🌜</span>
    </button>
  </header>
</template>

<script setup>

const props = defineProps({
  isDarkMode: Boolean,
});

const emit = defineEmits(["toggleDarkMode"]);

const toggleDarkMode = () => {
  emit("toggleDarkMode");
};
</script>
