<template>
  <h1>{{ msg }}</h1>
  <button type="button" @click="add(2)">count is: {{ count }}</button>
</template>


<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()
const count = ref(0)

const add = (n: number): void => {
  count.value += n
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
