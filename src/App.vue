<template>
  <transition name="fade">
    <Setup @game-init="gameInit" v-show="showSetup" :categories="categories" :difficulty="difficulty" />
  </transition>
  <Game :game-data="gameData" />
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
      showSetup: false,
      gameData: {
        title: null,
        level: null,
        titleSecret: '_________ _____ __',
        hint: 'American multinational automaker that has its main headquarters in Dearborn, Michigan, a suburb of Detroit.',
      }
    }
  },
  methods: {
    randomEl(el) {
      const length = Object.keys(el).length;
      return Math.floor(Math.random() * length + 1);
    },
    gameInit(category, level) {
      this.showSetup = false
      this.chosenDifficulty = level

      const randomCategory = category[this.randomEl(category)]
      const secretTitle = randomCategory.title.split('')

      secretTitle.forEach(el => {
        let letter;
        if(el === ' ') letter = ' ';
        else letter = '_'; 
        this.gameData.titleSecret += letter
      });
      gameData.hint = randomCategory.hint
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
