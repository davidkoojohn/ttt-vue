<template>
  <div class="board">
    <Square
        v-for="(item, index) of props.squares"
        :key="index"
        :val="item"
        :index="index"
        @whichClick="handleClick"
    />
  </div>
</template>

<script setup lang="ts">
import Square from "./Square.vue"

const props = defineProps<{
  squares: any[]
}>()

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
