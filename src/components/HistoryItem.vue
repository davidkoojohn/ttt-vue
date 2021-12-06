<template>
  <li :class="{ active: (props.step === props.index) }">
    <div>
      <template v-if="props.index !== 0">
        <i>{{ props.index }}.</i>
        <span class="pos">POS: ({{ props.pos[0] }}, {{ props.pos[1] }})</span>
      </template>
    </div>
    <button @click="handleClick(props.index)">
      {{ btnText }}
    </button>
  </li>
</template>

<script setup lang="ts">
import {computed} from "vue";

const props = defineProps<{
  index: number,
  pos: number[],
  step: number,
}>()

const btnText = computed(() => {
  if (props.index === 0) {
    return "Go to start"
  }
  return `Go to move #${props.index}`
})

const emit = defineEmits<{
  (e: "whichClick" , n: number): void
}>()
const handleClick = (n: number): void => {
  emit("whichClick", n)
}
</script>

<style scoped>
li {
  background: #000;
  margin-top: 5px;
  color: #fff;
  padding: 10px;
  display: flex;
  justify-content: space-between;
  box-sizing: border-box;
}

li.active {
  background-color: #eeeeee;
}

li i {
  color: red;
  font-weight: 700;
}

li .pos {
  color: #eee;
  margin-left: 20px;
}

li.active .pos {
  color: #2c3e50;
}
</style>
