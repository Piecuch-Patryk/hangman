<template>
  <div class="setup">
    <div class="inner">
      <div>
        <h2>Game Setup</h2>
        <p>Choose category and difficulty level from the options below.</p>
        <p>You've got to guess it, you'll hang otherwise.</p>
      </div>
      <div>
        <h3>Choose Category</h3>
        <label v-for="(value, key, index) in categories" :key="index">
          <input v-model="category" type="radio" :value="value" name="category">
          {{ key }}
        </label>
      </div>
      <div>
        <h3>Choose Difficulty Level</h3>
        <label v-for="(value, key, index) in difficulty" :key="index">
          <input v-model="level" type="radio" :value="value" name="difficulty">
          {{ key }}
        </label>
      </div>
      <div>
        <transition name="fade">
          <button v-show="category !== '' && level !== ''" @click="$emit('game-init', category, level)">Start Game</button>
        </transition>
      </div>
    </div>
    <div class="img-wrapper">
      <img src="@/assets/game/gibbet10.png" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Setup',
  props: {
    categories: Object,
    difficulty: Object,
  },
  data() {
    return {
      category: '',
      level: '',
    }
  },
}
</script>

<style lang="scss" scoped>
.setup {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #fff;
  text-align: center;

  .inner {
    width: 100%;
    background-color: #662d91;
    padding: 1rem;
    color: #ddd;
    
    h2 {
      font-size: 2.5rem;
      margin: 1rem auto;
    }

    label {
      text-transform: uppercase;
      margin: 0 1rem;
    }

    button {
      background-color: #fff;
      padding: .3rem 1rem;
      color: #333;
      border: none;
      border-radius: .5rem;
      margin: 2rem auto;
      font-size: 1.3rem;
    }
  }

  .img-wrapper {
    img {
      width: 100%;
    }
  }
}

@media (min-width: 768px) {
  .setup {
    .img-wrapper {
      margin-top: 4rem;
    }
  }
}
</style>