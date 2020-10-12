<template>
  <main class="game-wrapper">
    <GameBoard />
  </main>
</template>

<script>
import GameBoard from '@/components/GameBoard.vue'

export default {
  name: 'app',
  components: {
    GameBoard,
  }
}
</script>

<style lang="scss">
  :root {
    --white: #fff;
    --purple: #be8abf;
    --pink: #ea9abb;
    --orange: #fea5ad;
    --yellow: #f8c3af;
  }
  html {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
    border: 0;
  }
  body {
    margin: 0;
    padding: 0;
    border: 0;
  }
  .game-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0;
    padding: 0;
    background: var(--yellow);
    min-height: 100vh;
  }
</style>
