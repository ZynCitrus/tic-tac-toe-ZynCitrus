<script setup lang="ts">
import { ref, computed } from 'vue'

const playerOne = localStorage.getItem('playerOne');
const playerTwo = localStorage.getItem('playerTwo');

const player = ref(playerOne !== null ? playerOne : '');


const board = ref ([
  ['', '',''],
  ['', '',''],
  ['', '',''],
])

const currentPlayerName = computed(() => {
  return player.value === 'playerOne' ? playerOne : playerTwo;
});

const calculateWinner = (squares: any) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

const winner = computed (() => calculateWinner(board.value.flat()));

const makeMove = (x: any, y: any) => {
  if (winner.value) return;

  if (board.value[x][y] !== '') return;

  board.value[x][y] = player.value;

  player.value = player.value === 'playerOne' ? 'playerTwo' : 'playerOne';

  console.log(player.value)
}

const resetGame = () => {
  board.value = [
  ['', '',''],
  ['', '',''],
  ['', '',''],
]
player.value = 'playerOne'
}
</script>

<template>
<main class="pt-8 text-center dark: bg-gray-800 min-h-screen">
  <h1 class="mb-8 text-3xl font-bold uppercase">Tic Tac Toe</h1>


  <h3 class="text-xl mb-4">Det är {{ currentPlayerName }}s tur</h3>
    <div class="flex flex-col items-center mb-8">
			<div 
				v-for="(row, x) in board" 
				:key="x"
				class="flex">
				<div 
					v-for="(cell, y) in row" 
					:key="y" 
					@click="makeMove(x, y)" 
					:class="`border border-white w-24 h-24 hover:bg-gray-700 flex items-center justify-center material-icons-outlined text-4xl cursor-pointer ${cell === 'X' ? 'text-pink-500' : 'text-blue-400'}`">
					{{ cell === 'playerOne' ? 'X' : cell === 'playerTwo' ? 'O' : '' }}
				</div>
			</div>
		</div>
    <div class="text-center">
			<h2 v-if="winner" class="text-6xl font-bold mb-8">VINST!</h2>
			<button @click="resetGame" class="px-4 py-2 bg-pink-500 rounded uppercase font-bold hover:bg-pink-600 duration-300">Börja om spelet!</button>
		</div>
</main>
</template>

<style scoped>

</style>