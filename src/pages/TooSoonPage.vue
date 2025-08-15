<script setup>
import RectanglesIcon from "../components/RectanglesIcon.vue";
import { ref, defineEmits } from "vue";

const showClickPage = ref(false);
const emit = defineEmits(["close"]);
</script>
<template>
  <div class="too-soon-page" v-if="!showClickPage" @click="emit('close')">
    <RectanglesIcon />
    <h1 class="too-soon-page-text">Too Soon!</h1>
    <p class="small-text">Click to try again</p>
  </div>
</template>
<style scoped>
.too-soon-page {
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
