<template>
  <Transition
    enter-active-class="animate__animated animate__fadeInUp"
    leave-active-class="animate__animated animate__backOutDown"
  >
    <ErrorBanner v-if="errorMessage" />
  </Transition>

  <div class="background-img"></div>
  <router-view />
</template>

<script setup lang="ts">
import { computed } from "vue";

import ErrorBanner from "./components/ErrorBanner.vue";

import { useTodoStore } from "./store/todoStore";
const todoStore = useTodoStore();

const errorMessage = computed(() => todoStore.errorMessage);
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&family=Poppins:wght@500;700&display=swap");

:root {
  --bright-blue: #3a7bfd;
  --check-background: linear-gradient(#57ddff, #c058f3);

  --very-light-grey: #fafafa;
  --very-light-grayish-blue: #e4e5f1;
  --light-grayish-blue: #d2d3db;
  --dark-grayish-blue: #9394a5;
  --very-dark-grayish-blue: #484b6a;

  --very-dark-blue: #161722;
  --very-dark-desaturated-blue: #25273c;
  --light-grayish-blue-dark-mode: #cacde8;
  --light-grayish-blue-hover: #e4e5f1;
  --dark-grayish-blue-dark-mode: #777a92;
  --very-dark-grayish-blue-dark-mode: #4d5066;
  --very-dark-grayish-blue-dark-mode-second: #393a4c;
}

body {
  background-color: var(--very-dark-blue);
  position: relative;
  color: white;
  margin: 0;
}

.background-img {
  background-image: url("./assets/bg-desktop-dark.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  width: 100%;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  margin: 0;
  padding: 0;
}

#app {
  font-family: "Josefin Sans", sans-serif;

  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
