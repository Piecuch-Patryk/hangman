<template>
  <div class="game-over">
    <h3>Game Over ;(</h3>
    <div>
      <button @click="reload">Try Again</button>
    </div>
    <div>
      <img src="@/assets/game/gibbet10.png" alt="Hangman on a tree.">
    </div>
  </div>
</template>

<script>
export default {
  name: 'GameOver',
  methods: {
    reload() {
      window.location.reload()
    },
  },
}
</script>

<style lang="scss" scoped>
  .game-over {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background-color: #fff;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: center;

    h3 {
      font-size: 3rem;
    }

    button {
      background-color: #333;
      color: #ddd;
      font-size: 1.5rem;
      border: none;
      border-radius: .2rem;
      padding: .4rem 1rem;
      margin-bottom: 2rem;
    }

    img {
      width: 80%;
    }
  }
</style>