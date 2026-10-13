<template>
  <div class="game">
    <h1>Tris</h1>
    <div class="status">{{ status }}</div>
    <div class="board">
      <button
        v-for="(cell, i) in board"
        :key="i"
        class="cell"
        :class="[cell?.toLowerCase(), { win: winLine.includes(i) }]"
        :disabled="!!cell || !!winner"
        @click="play(i)"
        >
        {{ cell }}
      </button>
    </div>
    <div class="score">
      <span>X: {{ score.X }}</span>
      <span>Pareggi: {{ score.draw }}</span>
      <span>O: {{ score.O }}</span>
    </div>
    <button class="reset" @click="reset">Nuova partita</button>
  </div>
</template>

<script setup lang="ts">
  import { computed, ref } from 'vue'

type Player = 'X' | 'O'
type Cell = Player | null

const LINES = [
  [0, 1, 2], [3, 4, 5], [6, 7, 8],
  [0, 3, 6], [1, 4, 7], [2, 5, 8],
  [0, 4, 8], [2, 4, 6],
]

const board = ref<Cell[]>(Array(9).fill(null))
const current = ref<Player>('X') // X inizia sempre
const score = ref({ X: 0, O: 0, draw: 0 })

const winLine = computed<number[]>(() => {
  const b = board.value
  return LINES.find(([a, c, d]) => b[a!] && b[a!] === b[c!] && b[a!] === b[d!]) ?? []
})
const winner = computed<Cell>(() => (winLine.value.length ? board.value[winLine.value[0]!]! : null))
const isDraw = computed(() => !winner.value && board.value.every(Boolean))

const status = computed(() => {
  if (winner.value) return `Vince ${winner.value}!`
  if (isDraw.value) return 'Pareggio!'
  return `Turno di ${current.value}`
})
const play = (i:number) => {
  if (board.value[i] || winner.value) return
  board.value[i] = current.value
  if (winner.value) {
    score.value[winner.value]++
  } else if (isDraw.value) {
    score.value.draw++;
  } else {
    current.value = current.value === 'X' ? 'O' : 'X'
  }
}

const reset = () => {
  board.value = Array(9).fill(null)
  current.value = 'X'
}
</script>




<style scoped>
.game {
  text-align: center;
}
h1 {
  margin: 0 0 8px;
}
.status {
  font-size: 1.3rem;
  margin-bottom: 16px;
  min-height: 1.6em;
}
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  gap: 8px;
  justify-content: center;
}
.cell {
  width: 100px;
  height: 100px;
  font-size: 3rem;
  font-weight: bold;
  border: none;
  border-radius: 12px;
  background: #313244;
  color: #cdd6f4;
  cursor: pointer;
  transition: background 0.15s;
}
.cell:hover:not(:disabled) {
  background: #45475a;
}
.cell:disabled {
  cursor: default;
}
.cell.x {
  color: #f38ba8;
}
.cell.o {
  color: #89b4fa;
}
.cell.win {
  background: #a6e3a1;
  color: #1e1e2e;
}
.score {
  margin: 16px 0;
  display: flex;
  gap: 24px;
  justify-content: center;
}
.reset {
  padding: 10px 24px;
  font-size: 1rem;
  border: none;
  border-radius: 8px;
  background: #cba6f7;
  color: #1e1e2e;
  cursor: pointer;
}
</style>
