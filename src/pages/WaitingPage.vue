<script setup>
import ClickPage from "./ClickPage.vue";
import TooSoonPage from "./TooSoonPage.vue";
import RectanglesIcon from "../components/RectanglesIcon.vue";
import { ref, onMounted, watch } from "vue";

const showTooSoonPage = ref(false);
const showClickPage = ref(false);
const randomSeconds = ref(0);
let timeoutId = null;
function toggleClickPage() {
  showClickPage.value = true;
}
function toggleTooSoonPage() {
  showTooSoonPage.value = !showTooSoonPage.value;
  if (showTooSoonPage.value && timeoutId) {
    clearTimeout(timeoutId);
    timeoutId = null;
  }
}
function startRandomTimer() {
  if (timeoutId) clearTimeout(timeoutId);
  randomSeconds.value = (Math.floor(Math.random() * 3) + 3) * 1000;
  timeoutId = setTimeout(() => {
    toggleClickPage();
    timeoutId = null;
  }, randomSeconds.value);
}
onMounted(() => {
  startRandomTimer();
});
watch(showTooSoonPage, (newVal) => {
  if (!newVal && !showClickPage.value) {
    startRandomTimer();
  }
});
</script>

<template>
  <div
    v-if="!showClickPage && !showTooSoonPage"
    class="waiting-page"
    @click="toggleTooSoonPage"
  >
    <RectanglesIcon />
    <h1 class="waiting-page-text">Wait for green</h1>
  </div>
  <ClickPage v-if="showClickPage" />
  <TooSoonPage v-if="showTooSoonPage" @close="toggleTooSoonPage" />
</template>

<style scoped>
.waiting-page {
  top: 0;
  position: fixed;
  background-color: rgb(245, 39, 39);
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.waiting-page-text {
  margin-top: 0;
  font-size: clamp(3rem, 5vw, 5rem);
  color: #ffffff;
}
</style>
