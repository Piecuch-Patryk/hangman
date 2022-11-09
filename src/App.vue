<template>
  <transition name="fade">
    <Setup @game-init="gameInit" v-show="showSetup" :categories="categories" :difficulty="difficulty" />
  </transition>
  <Game :data="categories" />
</template>

<script>
import Game from './components/Game.vue'
import Setup from './components/Setup.vue'

export default {
  name: 'App',
  components: {
    Setup,
    Game,
  },
  data() {
    return {
      categories: {
        movie: {
          1: {
            title: 'The Hunger Games',
            hint: 'Every year in the ruins of what was once North America, the nation of Panem forces each of its twelve districts to send a teenage boy and girl to compete in...',
          },
          2: {
            title: 'Idiocracy',
            hint: 'Top-secret Human Hibernation Project. Pentagon picks the most average Americans they can find - private soldier and a prostitute and send them to the year 2505',
          }
        },
        car: {
          1: {
            title: 'Audi',
            hint: 'German automobile manufacturer that designs, engineers, produces, markets and distributes luxury vehicles. Member of the Volkswagen Group.',
          },
          2: {
            title: 'Ford',
            hint: 'American multinational automaker that has its main headquarters in Dearborn, Michigan, a suburb of Detroit.',
          }
        },
      },
      difficulty: {
        easy: 10,
        medium: 5,
        hard: 2,
      },
      showSetup: true,
    }
  },
  methods: {
    gameInit(category, level) {
      console.log(category)
      console.log(level)
      this.showSetup = false
    },
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
