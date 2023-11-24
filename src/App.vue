<script setup>
import { computed, ref, onMounted, onUnmounted } from 'vue'
import apiData from './assets/exampleData.json'
import ListItem from './components/ListItem.vue'

const showMenu = ref(false)
const defaultData = apiData.map((item) => {
  return {
    key: item.key,
    text: item.text
  }
})
const currentData = computed(() => (showMenu.value ? apiData : defaultData))

onMounted(() => {
  document.addEventListener('click', closeMenu)
})

onUnmounted(() => {
  document.removeEventListener('click', closeMenu)
})

function toggleMenu() {
  showMenu.value = !showMenu.value
}
function closeMenu() {
  showMenu.value = false
}
</script>

<template>
  <div class="wrapper">
    <header class="header">
      <div class="menu-wrapper">
        <button class="menu-bar" @click.stop="toggleMenu">
          <img alt="menu bar icon" class="bar-icon" src="@/assets/barIcon.svg" />
        </button>
      </div>
    </header>
    <!-- Menu -->
    <div class="menu-container" :class="showMenu ? 'menu-container__active' : ''">
      <ListItem :data="currentData" />
    </div>
    <!-- 九宮格 -->
    <div class="content"></div>
  </div>
</template>

<style scoped>
.wrapper {
  width: 100%;
  height: 100vh;
  max-width: 390px;
  margin: auto;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow-x: hidden;
}
.header {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 100%;
  justify-content: flex-end;
  background-color: white;
  padding: 10px;
}
.content {
  flex: 1;
  background-color: gray;
  display: flex;
  align-items: center;
}

.menu-bar {
  font-size: 1rem;
  width: 40px;
  height: 40px;
  flex: 40px 0 0;
  border-radius: 2px;
  background-color: transparent;
  border: none;
  padding: 0;
}

.bar-icon {
  width: 80%;
  height: 80%;
  object-fit: contain;
}

.menu-container {
  position: absolute;
  top: 0;
  right: 0;
  transform: translateX(100%);
  width: 50%;
  max-width: 250px;
  height: 100%;
  transition: transform 0.5s;
  z-index: 2;
  background-color: black;
}
.menu-container__active {
  transform: translateX(0);
  transition: transform 0.5s;
}
</style>
