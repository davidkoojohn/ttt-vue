<template>
  <header>
    <img alt="Vue logo" src="../assets/logo.png" />
    <span>Tic-Tac-Toe (三连棋)游戏</span>
  </header>
  <div class="game">
    <h3 class="status">{{ status }}</h3>
    <Board
        :squares="current.squares"
        @whichClick="handleClick"
    />
  </div>
</template>

<script setup lang="ts">
import {ref, reactive, computed} from "vue";
import Board from "../components/Board.vue"
import { calculateWinner } from "../tools.ts"

interface IHistory {
  squares: any[],
  pos: number[]
}

let history = reactive<IHistory[]>([
  {
    squares: Array(9).fill(null),
    pos: []
  },
])
const xIsNext = ref<boolean>(true)
const stepNumber = ref<number>(0)
const current = computed(() => history[stepNumber.value])
const status = computed(() => {
  const winner = calculateWinner(current.value.squares)
  if (winner) {
    return "Winner: " + winner.value
  } else {
    if (current.value.squares.every(item => !!item === true)) {
      return "No Winner!"
    } else {
      return `Next player: ${ xIsNext.value ? "X" : "O" }`;
    }
  }
})

const handleClick = (n: number):void => {
  const squares = current.value.squares.slice();
  squares[n] = xIsNext.value ? "X" : "O"
  history.push({
    squares: squares,
    pos: [parseInt(String(n / 3)) + 1, n % 3 + 1] // [行, 列]
  })
  stepNumber.value += 1
  xIsNext.value = !xIsNext.value
}

</script>

<style scoped>
header {
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #282c34;
}

header img {
  height: 70px;
  margin-right: 20px;
}

header span {
  font-size: 30px;
  font-weight: 200;
  color: #eee;
}

.game {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

.status {
  font-size: 30px;
  font-weight: 700;
  color: #fff;
}
</style>
