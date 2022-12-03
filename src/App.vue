<template>
  <main class="min-h-screen dark:bg-slate-900 dark:text-white">
    <Header>Vue JS 3 Tic Tac Toe</Header>
    <Board/>
  </main>
</template>

<script setup>
import Board from '@/components/Board.vue';
import Header from '@/components/Header.vue';
</script>
