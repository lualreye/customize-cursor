<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

let x = ref(0);
let y = ref(0);

const mouseMove = () => window.addEventListener("mousemove", mouseLocation)
const mouseMoveOut = () => window.removeEventListener("mousemove", mouseLocation)

const mouseLocation = (event) => {
  x.value = event.pageX - 25 + 'px'
  y.value = event.pageY - 25 + 'px'
}

onMounted(() => {
  mouseMove()
})

onUnmounted(() => {
  mouseMoveOut()
})

</script>

<template>
  <div class="cursor-layout">
    <div :style="{ top:y, left:x }" class="cursor" />
  </div>
</template>

<style>
.cursor-layout {
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99;
  background: transparent;
  pointer-events: none;
}
.cursor {
  width: 50px;
  height: 50px;
  position: absolute;
  z-index: 999;
  border-radius: 50%;
  pointer-events: none;
  animation: pulse 1500ms infinite;
}
@keyframes pulse {
  0% {
    transform: scale(1);
    border: 2px solid green;
  }
  50% {
    transform: scale(2);
    border: 2px solid yellow;
  }
  100% {
    transform: rotate(1);
    border: 2px solid green;
  }
}
</style>