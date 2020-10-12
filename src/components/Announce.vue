<template>
  <div></div>
</template>

<script>
export default {
  name: 'Announce',
  props: {
    currentSound: {
      type: Object
    },
    replaySound: {
      type: Boolean
    }
  },
  methods: {
    playSound(sound) {
      const media = new Audio(sound)
      media.play()
    }
  },
  watch: {
    currentSound(piece) {
      this.playSound(piece.sound)
    },
    replaySound(replaySound) {
      if (replaySound) this.playSound(this.currentSound.sound)
    }
  },
}
</script>

<style>

</style>