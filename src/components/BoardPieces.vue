<template>
  <div class="pieces">
    <div
      class="pieces__piece"
      v-for="piece in pieces"
      :key="`piece-${piece.char}`"
      @click="makeGuess(piece.char)"
      :style="piece.disabled && 'opacity: 0; pointer-events: none;'"
    >
      {{ piece.char }}
    </div>
    <div 
      v-if="hasWon || !hasBegunGame"
      class="pieces__new-game-wrapper"
    >
      <button
        class="pieces__new-game-btn"
        @click="startNewGame()"
      >
        Play!
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BoardPieces',
  props: {
    pieces: {
      type: Array
    },
    currentLetter: {
      type: Object
    },
    hasWon: {
      type: Boolean
    },
    hasBegunGame: {
      type: Boolean
    }
  },
  methods: {
    startNewGame() {
      this.$emit('startNewGame')
    },
    makeGuess(char) {
      if (this.currentLetter.char === char) {
        this.$emit('advanceLetter', char)
      } else {
        this.$emit('replaySound')
      }
    },
  }
}
</script>

<style lang="scss">
  .pieces {
    display: flex;
    flex-wrap: wrap;
    position: relative;
    &__piece {
      font-size: 2rem;
      color: var(--white);
      background: var(--purple);
      cursor: pointer;
      width: 27%;
      height: 83px;
      flex-grow: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      border: 3px solid var(--pink);
      transition: 0.3s all ease;
      &:hover {
        background: var(--pink);
        border-color: var(--purple);
      }
    }
    &__new-game-wrapper {
      position: absolute;
      top: 0;
      right: 0;
      background: rgba(0,0,0,0.7);
      height: 800px;
      width: 800px;
      display: flex;
      justify-content: center;
      align-items: center;
      transition: 0.5s all ease;
    }
    &__new-game-btn {
      padding: 50px 100px;
      font-size: 3rem;
      color: var(--white);
      background: var(--pink);
      border: 15px solid var(--purple);
      transition: 0.3s all ease;
      cursor: pointer;
      &:hover {
        opacity: 0.8;
      }
    }
  }
</style>