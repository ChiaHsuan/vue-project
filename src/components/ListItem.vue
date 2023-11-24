<script setup>
import { ref } from 'vue'

defineProps({
  data: {
    type: Array,
    required: true
  }
})

const currentChildren = ref([])
const currentIndex = ref(-1)

function toggleChildren(item) {
  if (currentIndex.value !== item.index) {
    // open sub menu
    currentChildren.value = item.item.children || []
    currentIndex.value = item.index
  } else {
    // close sub menu
    currentIndex.value = -1
    currentChildren.value = []
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
}
.link-text {
  display: inline-block;
  padding: 0.5rem 0;
}
.active-text {
  color: yellow;
}
.inactive-text {
  color: #fff;
}
</style>
