<script setup>
import { ref, toRefs, watch } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true
  }
})

const { data: reactiveData } = toRefs(props)
const currentChildren = ref([])
const currentIndex = ref(-1)

/**
 * 若 parent 資料有變化, 移除所有的 sub menu
 */
watch(reactiveData, () => {
  reset()
})

/**
 * Reset Data
 */
function reset() {
  currentIndex.value = -1
  currentChildren.value = []
}

function toggleChildren(item) {
  if (currentIndex.value !== item.index) {
    // open sub menu
    currentChildren.value = item.item.children || []
    currentIndex.value = item.index
  } else {
    // close sub menu
    reset
  }
}
</script>

<template>
  <ul class="list">
    <li
      v-for="(item, index) in data"
      :key="item.key"
      @click.stop="toggleChildren({ item, index }, $event)"
    >
      <a
        href="#"
        class="link-text"
        :class="currentIndex === index ? 'active-text' : 'inactive-text'"
        >{{ item.text }}</a
      >
      <template v-if="currentIndex === index && currentChildren.length !== 0">
        <ListItem :data="currentChildren" />
      </template>
    </li>
  </ul>
</template>

<style scoped>
.list {
  list-style: none;
  padding: 0.5rem 0 0.5rem 0.8rem;
  background-color: rgb(187, 185, 185);
}
.link-text {
  display: inline-block;
  padding: 0.5rem 0;
  width: 100%;
}
.active-text {
  color: yellow;
}
.inactive-text {
  color: #fff;
}
</style>
