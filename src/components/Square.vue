<template>
  <button @click="handleClick(props.index)">
    {{ props.val }}
  </button>
</template>

<script setup lang="ts">
const props = defineProps<{
  val: any,
  index: number
}>()

const emit = defineEmits<{
  (e: "whichClick" , n: number): void
}>()

const handleClick = (n: number):void => {
  emit("whichClick", n)
}
</script>

<style scoped>
button {
  box-sizing: border-box;
  width: 70px;
  height: 70px;
  border: 2px solid #282c34;
  background-color: #fff;
  font-size: 24px;
  font-weight: 700;
}
</style>
