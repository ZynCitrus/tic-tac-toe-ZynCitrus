<script setup lang="ts">
import { ref } from 'vue';
import PlayerName from './components/PlayerName.vue';

const playerOne = ref('');
const playerTwo = ref('');

const updatePlayerNames = (nameOne: string, nameTwo: string) => {
  playerOne.value = nameOne;
  playerTwo.value = nameTwo;
};
</script>

<template>
<main class="pt-8 text-center dark: bg-gray-800 min-h-screen">
  <PlayerName></PlayerName>
</main>
</template>

<style scoped>

</style>