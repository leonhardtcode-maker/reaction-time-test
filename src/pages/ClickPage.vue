<script setup>
import RectanglesIcon from "../components/RectanglesIcon.vue";
import ResultPage from "./ResultPage.vue";
import { ref, onMounted } from "vue";

const showResultPage = ref(false);
const reactionTimeResult = ref(0);
const startTime = ref(0);
function toggleResultPage() {
  const endTime = performance.now();
  reactionTimeResult.value = Math.floor(endTime - startTime.value);
  showResultPage.value = !showResultPage.value;
  console.log(reactionTimeResult.value);
}
function startTimer() {
  startTime.value = performance.now();
}
onMounted(() => {
  startTimer();
});
</script>
<template>
  <div class="click-page" v-if="!showResultPage" @click="toggleResultPage">
    <RectanglesIcon />
    <h1 class="click-page-text">Click !!!</h1>
  </div>
  <ResultPage v-if="showResultPage" :result="reactionTimeResult" />
</template>
<style scoped>
.click-page {
  top: 0;
  position: fixed;
  background-color: rgb(11, 255, 48);
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
