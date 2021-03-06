<template>
  <header>
    <img alt="Vue logo" src="../assets/logo.png" />
    <span>Tic-Tac-Toe (三连棋)游戏</span>
  </header>
  <div class="game">
    <h3 class="status">{{ status }}</h3>
    <Board
        :squares="current.squares"
        :line="line"
        @whichClick="handleClick"
    />
    <div class="history">
      <ol>
        <HistoryItem
            v-for="(item, index) of history"
            :key="index"
            :index="index"
            :pos="item.pos"
            :step="stepNumber"
            @whichClick="moveHistory"
        />
      </ol>
    </div>
  </div>
</template>

<script setup lang="ts">
import {ref, reactive, computed} from "vue";
import Board from "../components/Board.vue"
import HistoryItem from "../components/HistoryItem.vue"
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
const line = ref<number[]>([])
const current = computed(() => history[stepNumber.value])
const status = computed(() => {
  const winner = calculateWinner(current.value.squares)
  if (winner) {
    line.value = winner.line
    return "Winner: " + winner.value
  } else {
    line.value = []
    if (current.value.squares.every(item => !!item === true)) {
      return "No Winner!"
    } else {
      return `Next player: ${ xIsNext.value ? "X" : "O" }`;
    }
  }
})

const handleClick = (n: number):void => {
  if (calculateWinner(current.value.squares) || current.value.squares[n]) return
  const squares = current.value.squares.slice();
  squares[n] = xIsNext.value ? "X" : "O"
  history.push({
    squares: squares,
    pos: [parseInt(String(n / 3)) + 1, n % 3 + 1] // [行, 列]
  })
  stepNumber.value += 1
  xIsNext.value = !xIsNext.value
}

const moveHistory = (n: number): void => {
  stepNumber.value = n
  history.splice(n + 1)
  xIsNext.value = (n % 2) === 0
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

.history ol {
  width: 500px;
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
