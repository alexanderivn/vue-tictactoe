<template>
  <section class="py-8 text-center">
    <div>
      <h3>Player {{ player }}'s turn</h3>
    </div>
  </section>

  <section>
    <div class="flex flex-col items-center mb-8">
      <div v-for="(row,x) in board" :key="x" class="flex">
        <div v-for="(cell,y) in row"
             :key="y" @click="makeMove(x,y)"
             :class="`border border-white w-20 h-20 hover:bg-gray-700 flex items-center material-icons-outlined justify-center text-4xl cursor-pointer ${cell === 'X' ? 'text-red-500' : 'text-blue-500'}`">
          {{ cell === 'X' ? 'close' : cell === 'O' ? 'circle' : '' }}
        </div>
      </div>

      <div class="py-8 space-y-4 flex flex-col justify-center">
        <h2 v-if="winner" class="text-4xl font-bold mb-8">Player {{ winner }} wins!</h2>
        <ButtonPrimary @click="resetGame"> Play Again!</ButtonPrimary>
      </div>
    </div>
  </section>
</template>

<script setup>
import {computed, ref} from "vue";
import ButtonPrimary from '@/components/ButtonPrimary.vue';


const player = ref('X')
const board = ref([
  ['', '', ''],
  ['', '', ''],
  ['', '', ''],
]);

const calculateWinner = (board) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
      return board[a];
    }
  }
  return null;
}

const winner = computed(() => calculateWinner(board.value.flat()));

const makeMove = (x, y) => {
  if (winner.value) return;

  if (board.value[x][y] !== '') return
  board.value[x][y] = player.value

  player.value = player.value === 'X' ? 'O' : 'X'
}

const resetGame = () => {
  board.value = [
    ['', '', ''],
    ['', '', ''],
    ['', '', ''],
  ];

  // player.value = 'X';

  const playerStrings ='XO';
  function randomizeTurn(length) {
    let result = '';
    const charactersLength = playerStrings.length;
    for ( let i = 0; i < length; i++ ) {
      result += playerStrings.charAt(Math.floor(Math.random() * charactersLength ));
    }
    return player.value = result;
  }
  console.log(randomizeTurn(1));
}

</script>
