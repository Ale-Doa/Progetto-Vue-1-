<template>
  <mian class="home">
    <h1 class="title">Tic Tac Toe</h1>

    <div class="container">
      <button v-for="(value, index) in squares" :key="index" @click="symbolAssign(index)" class="block">{{ value
        }}</button>
    </div>

    <h2 class="turnCounter">Turno: {{ turnCounter }}</h2>
    <h2 class="winnerMessage" v-if="winnerMessage">{{ winnerMessage }}</h2>

    <button @click="reset" class="resetButton">RESET</button>
  </mian>
</template>

<script setup>
import { ref } from 'vue'

const turnCounter = ref(1)
const squares = ref(Array(9).fill(''))
const winnerMessage = ref('')

function checkWinner() {
  const winningCombinations = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8],
    [0, 3, 6], [1, 4, 7], [2, 5, 8],
    [0, 4, 8], [2, 4, 6]
  ];

  for (const combination of winningCombinations) {
    const [a, b, c] = combination
    if (squares.value[a] && squares.value[a] === squares.value[b] && squares.value[a] === squares.value[c]) {
      return squares.value[a] //restituisce il simbolo del vincitore
    }
  }
  return null
}

function symbolAssign(index) {
  if (squares.value[index] !== '' || winnerMessage.value !== '') return
  squares.value[index] = turnCounter.value % 2 === 0 ? 'O' : 'X'
  const winner = checkWinner()
  if (winner) {
    winnerMessage.value = `${winner} È il vincitore!`
    setTimeout(reset, 2000)
  } else {
    turnCounter.value++
  }
}

function reset() {
  turnCounter.value = 1
  squares.value = Array(9).fill('')
  winnerMessage.value = ''
}
</script>

<style>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  height: 300px;
  width: 300px;
  border: 1px solid black;

  margin: 0 auto;
}

.title {
  font-size: 70px;
  margin-top: 8%
}

.turnCounter {
  font-size: 50px;
}

.block {
  background-color: antiquewhite;
  border: solid;
  border-color: gray;
  border-width: 1px;
  cursor: pointer;
  font-size: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  height: 100px;
}

.resetButton {
  font-size: 30px;
  padding: 15px;
  cursor: pointer;
  border-radius: 15px;
  background-color: antiquewhite;
}

.winnerMessage {
  position: fixed;
  top: 33%;
  left: 33%;
  font-size: 5vw;
  background-color: antiquewhite;
  border: 1px solid black;
  border-radius: 25px;
  box-shadow: 5px 5px 5px gray;
}

@media (max-width: 450px) {
  .winnerMessage {
    top: 28%;
    left: 3%;
    font-size: 6vh;
  }
}
</style>