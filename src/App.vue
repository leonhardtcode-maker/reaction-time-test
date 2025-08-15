<script setup>
import HeaderLogo from "./components/HeaderLogo.vue";
import WaitingPage from "./pages/WaitingPage.vue";
import { ref, provide } from "vue";

const showWaitingPage = ref(false);
function toggleWaitingPage() {
  showWaitingPage.value = !showWaitingPage.value;
}
provide("goToHomepage", toggleWaitingPage);
</script>

<template>
  <div class="home-page" @click="toggleWaitingPage" v-if="!showWaitingPage">
    <header>
      <HeaderLogo />
      <h1 class="header-title">Reaction Time Test</h1>
    </header>
    <main>
      <h3 class="main-text">
        When the redbox turns green, click as quickly as you can.
      </h3>
      <h3 class="main-text">Click anywhere to start</h3>
    </main>
  </div>
  <WaitingPage v-if="showWaitingPage" />
</template>

<style scoped>
.home-page {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
header {
  display: flex;
  flex-direction: column;
  align-items: center;
}
main {
  padding: 0.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.header-title {
  margin-top: 2vw;
  font-size: clamp(2rem, 3vw, 4rem);
  margin-bottom: 20px;
  @media (prefers-color-scheme: light) {
    color: #213547;
  }
}
.main-text {
  margin-top: 0;
  margin-bottom: 0;
  font-weight: 400;
  font-size: clamp(0.8rem, 1.2vw, 2rem);
}
</style>
