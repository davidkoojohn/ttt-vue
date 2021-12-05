<template>
  <button
      :class="{ red: props.bgRed }"
      @click="handleClick(props.index)"
  >
    {{ props.value }}
  </button>
</template>

<script setup lang="ts">
const props = defineProps<{
  value: any,
  index: number,
  bgRed: boolean
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

button.red {
  background: red;
}
</style>
