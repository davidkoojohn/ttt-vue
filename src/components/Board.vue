<template>
  <div class="board">
    <Square
        v-for="(item, index) of props.squares"
        :key="index"
        :value="item"
        :index="index"
        :bgRed="isRedBg(index)"
        @whichClick="handleClick"
    />
  </div>
</template>

<script setup lang="ts">
import Square from "./Square.vue"

const props = defineProps<{
  squares: any[],
  line: number[]
}>()

const isRedBg = (n) => props.line.includes(n)

const emit = defineEmits<{
  (e: "whichClick" , n: number): void
}>()

const handleClick = (n: number):void => {
  emit("whichClick", n)
}

</script>

<style scoped>
.board {
  width: 210px;
  display: flex;
  flex-wrap: wrap;
}
</style>
