<script setup lang="ts">
import { computed, ref, type ComputedRef, type Ref } from 'vue'

// data
let hour = new Date().getHours()

let judge: boolean = init()
let isDark: Ref<boolean> = ref<boolean>(judge)

function init() {
  if ((hour > 18 && hour <= 25) || hour < 6) {
    localStorage.setItem('theme', 'dark')
    return true
  } else {
    localStorage.setItem('theme', 'light')
    return false
  }
}
const containerClass: ComputedRef = computed(() => {
  return {
    'container-center': true,
    'dark-theme': isDark.value,
    'light-theme': !isDark.value
  }
})

const changeMode = () => {
  isDark.value = !isDark.value
  if (isDark.value === true) {
    localStorage.setItem('theme', 'dark')
  } else {
    localStorage.setItem('theme', 'light')
  }
}
</script>

<template>
  <div :class="containerClass">
    <button class="mode-btn" @click="changeMode">click mode</button>
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  width: 100%;
  min-height: 100vh;
}

.dark-theme {
  --background-color-primary: #222;
  --button-background-color: #ebebeb;
  --button-text-color: #222;
}
.light-theme {
  --background-color-primary: #ebebeb;
  --button-background-color: #222;
  --button-text-color: #ebebeb;
}
.light-theme,
.dark-theme {
  transition: 0.3s ease-in-out;
}
.container-center {
  width: 100%;
  min-height: 100vh;
  position: relative;
  background-color: var(--background-color-primary);
}
.mode-btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90px;
  height: 50px;
  border-radius: 5%;
  border: 0;
  font-family: 'Courier New', Courier, monospace;
  font-size: 15px;
  background-color: var(--button-background-color);
  color: var(--button-text-color);
  font-weight: 500;
  margin: 0;
}
.mode-btn:hover {
  background-color: grey;
  transition: 0.2s ease-in-out;
  cursor: pointer;
}
</style>
