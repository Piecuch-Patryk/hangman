<template>
  <div class="keyboard" ref="keyboardContainer">
    <div>
      <button @click="$emit('validate-letter', $event)" v-for="btn in row1" :key="btn" class="letter">{{ btn }}</button>
    </div>
    <div>
      <button @click="$emit('validate-letter', $event)" v-for="btn in row2" :key="btn" class="letter">{{ btn }}</button>
    </div>
    <div>
      <button @click="$emit('validate-letter', $event)" v-for="btn in row3" :key="btn" class="letter">{{ btn }}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Keyboard',
  data() {
    return {
      row1: 'QWERTYUIOP'.split(''),
      row2: 'ASDFGHJKL'.split(''),
      row3: 'ZXCVBNM'.split(''),
    }
  },
}
</script>

<style lang="scss" scoped>
.keyboard {
  margin-top: 1rem;
  .letter {
    background-color: #662d91;
    color: #fff;
    width: 1.5rem;
    height: 1.5rem;
    line-height: 1.5rem;
    border: none;
    border-radius: .2rem;
    margin: .1rem;
    transition: scale .2s ease;

    &.success {
      transform: scale(.9);
      background-color: green;
    }

    &.failure {
      background-color: red;
    }
  }
}
</style>