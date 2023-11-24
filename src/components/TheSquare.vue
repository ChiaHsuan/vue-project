<script setup>
import { ref } from 'vue'

const square = ref(new Array(9))
</script>

<template>
  <div class="flex-wrapper">
    <div
      class="sqaure"
      v-for="(item, index) in square"
      :key="index"
      :class="[2, 4, 8].includes(index) ? 'sqaure__fade' : ''"
    ></div>
    <div class="dot top"></div>
    <div class="dot bottom"></div>
  </div>
</template>

<style scoped>
.flex-wrapper {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  position: relative;
  overflow: hidden;
  justify-content: space-around;
}
.sqaure {
  height: 100px;
  width: 30%;
  margin: 5px 0;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113, 81, 95, 1) 81%, rgba(0, 0, 0, 1) 100%);
  justify-content: space-evenly;
}

.sqaure__fade {
  animation: fade 2s infinite 1s;
}

@keyframes fade {
  0% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
  100% {
    opacity: 1;
  }
}

.dot {
  width: 30px;
  height: 30px;
  background-color: #a5f12b;
  position: absolute;
  border-radius: 50%;
  animation: slide 2s infinite 1s;
  z-index: 1;
  left: calc(16.66% - 15px);
}
.top {
  top: calc(16.66% - 15px);
}

.bottom {
  top: calc(83.33% - 15px);
}

@keyframes slide {
  0% {
  }
  80% {
    left: calc(83.33% - 15px);
  }
  100% {
    left: 100%;
  }
}
</style>
