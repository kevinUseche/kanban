<script setup>
import Board from './components/Board.vue';
</script>

<template>
  <header class="site-header">
    <h2 class="title-board">kanban board</h2>
  </header>
  <div class="container">
    <Board />
  </div>
</template>

<style scoped>
  .site-header{
    background-color: var(--dark-green);
    padding: 2rem;
  }
  .title-board{
    color: var(--white);
    text-align: center;
    text-transform: capitalize;
  }
  .container{
    width: 95%;
    max-width: 120rem;
    margin: 0 auto;
  }
</style>
