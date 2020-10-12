<template>
  <section 
    class="board"
    :style="`background-image: url(${background})`"
  >
    <BoardPieces 
      :pieces="pieces"
      :currentLetter="currentLetter"
      :hasWon="hasWon"
      :hasBegunGame="hasBegunGame"
      @advanceLetter="advanceLetter"
      @replaySound="playSound"
      @startNewGame="startNewGame"
    />
  </section>
</template>

<script>
import BoardPieces from './BoardPieces.vue'
import alphabet from './alphabet'

export default {
  name: 'GameBoard',
  components: {
    BoardPieces,
  },
  data() {
    return {
      backgrounds: [
        require('@/assets/backgrounds/leopard_cub.jpg'),
        require('@/assets/backgrounds/t_rex.jpg'),
        require('@/assets/backgrounds/elsa.jpeg'),
        require('@/assets/backgrounds/olaf.jpg'),
      ],
      background: '',
      pieces: alphabet,
      currentLetter: '',
      hasBegunGame: false,
    }
  },
  computed: {
    hasWon() {
      const enabled = this.pieces.filter(piece => !piece.disabled)
      return enabled.length === 0
    }
  },
  methods: {
    updateBackground() {
      const { backgrounds } = this
      this.background = backgrounds[Math.floor(Math.random() * backgrounds.length)]
    },
    advanceLetter(char) {
      const guessed = this.pieces.find(piece => piece.char === char)
      guessed.disabled = true
      const enabled = this.pieces.filter(piece => !piece.disabled)
      this.currentLetter = enabled[Math.floor(Math.random() * enabled.length)] || {}
      this.playSound()
    },
    playSound() {
      const media = new Audio(this.currentLetter.sound)
      media.play()
    },
    startNewGame() {
      this.pieces.map(piece => piece.disabled = false)
      this.currentLetter = this.pieces[Math.floor(Math.random() * this.pieces.length)]
      this.updateBackground()
      this.hasBegunGame = true
      this.playSound()
    }
  }
}
</script>

<style lang="scss" scoped>
  .board {
    height: 800px;
    width: 800px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
  }
</style>
