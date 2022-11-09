<template>
  <div class="game">
    <div>
      <h1>Hangman</h1>
      <h2>Don't do it at home!</h2>
    </div>
    <div class="img-wrapper">
      <img :src="require(`@/assets/game/gibbet${index}.png`)" alt="Hangman on a tree.">
    </div>
    <div>
      <p class="secret">{{ gameData.titleSecret }}</p>
    </div>
    <div class="hint">
      <p>{{ gameData.hint }}</p>
    </div>
    <div>
      <Keyboard @validate-letter="$emit('validate-letter', $event)" />
    </div>
  </div>
</template>

<script>
import Keyboard from '@/components/Keyboard.vue'

export default {
  name: 'Game',
  data() {
    return {
      hint: false,
    }
  },
  components: {
    Keyboard,
  },
  props: {
    gameData: Object,
    index: Number,
  }
}
</script>

<style scoped lang="scss">
.game {
  text-align: center;

  h1 {
    margin: 0;
    font-size: 2.5rem;
  }
  h2 {
    font-size: 1rem;
    margin: 0;
  }

  .secret {
    letter-spacing: .3rem;
  }

  .img-wrapper {
    img {
      width: 90%;
      margin-bottom: 1rem;
    }
  }
}

@media (min-width: 768px) {
  .game {

    .img-wrapper {

      img {
        width: 50%;
      }
    }

    .hint {
      width: 50%;
      margin: 2rem auto;
      font-size: 1.5rem;
    }
  }
}
</style>
