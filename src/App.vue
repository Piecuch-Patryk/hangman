<template>
  <transition name="fade">
    <Setup @game-init="gameInit" v-show="showSetup" :categories="categories" :difficulty="difficulty" />
  </transition>

  <Game :index="image" :game-data="gameData" @validate-letter="validate" />

  <transition name="fade">
    <GameResult v-show="showGameResult" :msg="gameResult" :gameOver="gameOver" :gameWon="gameWon" />
  </transition>
</template>

<script>
import Setup from './components/Setup.vue'
import Game from './components/Game.vue'
import GameResult from './components/GameResult.vue'

export default {
  name: 'App',
  components: {
    Setup,
    Game,
    GameResult,
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
      gameData: {
        title: '',
        level: null,
        titleSecret: '',
        hint: '',
      },
      image: 0,
      showGameResult: false,
      gameResult: '',
      gameWon: false,
    }
  },
  methods: {
    gameOver() {
      this.gameResult = 'Game Over! ;('
      this.showGameResult = true
    },
    setImage(boolean) {
      if(this.image >= 9) {
        setTimeout(() => {
          this.gameOver()
        }, 500)
        return
      }
      if(boolean) this.image++
    },
    showValidLetter(singleLetter) {
      let letter = singleLetter
      const secretSentence = this.gameData.title.toLowerCase().split('')
      const hiddenSecretSentence = this.gameData.titleSecret.split('')
      const indexes = [];
      
      secretSentence.forEach((el, i) => {
          if(el === letter) indexes.push(i);
      });

      indexes.forEach(el => {
          if(el === 0) letter = letter.toUpperCase();
          else letter = letter.toLowerCase();
          hiddenSecretSentence[el] = letter;
      });

      this.gameData.titleSecret = hiddenSecretSentence.join('')

      if(!hiddenSecretSentence.includes('_')) {
        this.showGameResult = true
        this.gameResult = 'Congratulations!'
        this.gameWon = true
      }
    },
    validate($event) {
      const letter = $event.target.innerText.toLowerCase()
      const secretTitle = this.gameData.title.toLowerCase().split('')
      const isValid = secretTitle.includes(letter)
      if (isValid) {
        this.showValidLetter(letter);
        $event.target.classList.add('success')
      }else {
        $event.target.classList.add('failure')
        this.setImage(true)
        setTimeout(() => {
          $event.target.classList.remove('failure')
        }, 200)
      }
    },
    randomEl(el) {
      const length = Object.keys(el).length;
      return Math.floor(Math.random() * length + 1);
    },
    gameInit(category, level) {
      this.showSetup = false
      this.chosenDifficulty = level

      const randomCategory = category[this.randomEl(category)]
      this.gameData.title = randomCategory.title.toLowerCase()

      const secretTitle = randomCategory.title.split('')

      secretTitle.forEach(el => {
        let letter;
        if(el === ' ') letter = ' ';
        else letter = '_'; 
        this.gameData.titleSecret += letter
      });
      this.gameData.hint = randomCategory.hint
    },
  },
  mounted() {
    this.setImage(false)
  },
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
