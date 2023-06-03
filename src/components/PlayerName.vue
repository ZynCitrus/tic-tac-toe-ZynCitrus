<script setup lang="ts">
import { ref, onMounted } from 'vue';
import GameBoard from './GameBoard.vue';

const playerOne = ref('');
const playerTwo = ref('');
const saved = ref(false);


onMounted(() => {
  const savedPlayerOne = localStorage.getItem('playerOne');
  const savedPlayerTwo = localStorage.getItem('playerTwo');

  if (savedPlayerOne) {
    playerOne.value = savedPlayerOne;
  }

  if (savedPlayerTwo) {
    playerTwo.value = savedPlayerTwo;
  }
});

const saveNames = () => {
  localStorage.setItem('playerOne', playerOne.value);
  localStorage.setItem('playerTwo', playerTwo.value);
  saved.value = true;
};
</script>


<template>
    <div class="flex flex-col">
      <div v-if="!saved">
        <div class="mb-4">
          <label for="playerOneName" class="mr-2">Spelare 1:</label>
          <input id="playerOneName" v-model="playerOne" class="border border-gray-300 rounded p-1" />
        </div>
        <div class="mb-4">
          <label for="playerTwoName" class="mr-2">Spelare 2:</label>
          <input id="playerTwoName" v-model="playerTwo" class="border border-gray-300 rounded p-1" />
        </div>
        <button @click="saveNames">Spela</button>
      </div>
     <div v-else> 
        <GameBoard :playerOne="playerOne" :playerTwo="playerTwo" />
      </div>
    </div>
  </template>