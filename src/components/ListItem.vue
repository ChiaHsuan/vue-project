<script setup>
import { ref } from 'vue'

defineProps({
  data: {
    type: Array,
    required: true
  }
})

const currentChildren = ref([{ key: 'testKey', name: 'testName' }])
const currentIndex = ref(-1)

function toggleChildren(item) {
  currentChildren.value = item.item.children || []
  currentIndex.value = item.index
}
</script>

<template>
  <ul style="background-color: gray; color: black">
    <li
      v-for="(item, index) in data"
      :key="item.key"
      @click.stop="toggleChildren({ item, index }, $event)"
    >
      <div>{{ item.text }}</div>
      <template v-if="currentIndex === index">
        <ListItem :data="currentChildren" />
      </template>
    </li>
  </ul>
</template>

<style scoped></style>
