<template>
  <h1>Hello Sudoku Player!</h1>
  <main>
    <GamePage />
  </main>
</template>

<script>

import GamePage from "@/pages/GamePage.vue";

export default {
  name: 'App',
  components: {
    GamePage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
