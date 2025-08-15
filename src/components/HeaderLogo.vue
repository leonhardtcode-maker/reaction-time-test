<script setup>
import { ref, onMounted } from "vue";

const isDarkMode = ref(true);
const imageSrc = ref("");

function updateImage() {
  if (isDarkMode.value) {
    imageSrc.value = "./src/assets/flash_icon_dark_mode.svg";
  } else {
    imageSrc.value = "./src/assets/flash_icon_light_mode.svg";
  }
}
onMounted(() => {
  // Cek mode saat mount
  isDarkMode.value = window.matchMedia("(prefers-color-scheme: dark)").matches;
  updateImage();

  // Listen perubahan mode secara real-time
  window
    .matchMedia("(prefers-color-scheme: dark)")
    .addEventListener("change", (e) => {
      isDarkMode.value = e.matches;
      updateImage();
    });
});
</script>
<template>
  <img class="header-image-icon" :src="imageSrc" alt="header-flash-logo" />
</template>
<style scoped>
.header-image-icon {
  min-width: 100px;
  max-width: 12vw;
  animation: breathingAnimations 2s infinite ease-in-out;
}
@media (prefers-color-scheme: dark) {
  @keyframes breathingAnimations {
    0%,
    100% {
      filter: opacity(1);
    }
    50% {
      filter: opacity(0.6);
    }
  }
}
@media (prefers-color-scheme: light) {
  @keyframes breathingAnimations {
    0%,
    100% {
      filter: opacity(1);
    }
    50% {
      filter: opacity(0.88);
    }
  }
}
</style>
