<script setup>
import RectanglesIcon from "../components/RectanglesIcon.vue";
import { inject } from "vue";
const goToHomepage = inject("goToHomepage");
defineProps({
  result: Number,
});
</script>
<template>
  <div class="result-page" @click="goToHomepage">
    <RectanglesIcon />
    <h1 class="result-page-text">{{ result }} ms</h1>
    <p class="result-page-small-text">Click to try again</p>
  </div>
</template>
<style scoped>
.result-page {
  top: 0;
  position: fixed;
  background-color: rgb(21, 44, 254);
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
