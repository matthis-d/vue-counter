<template>
  <button :class="{ negative: isNegative }" @click.prevent="updateScore">{{prefix}} {{score}}</button>
</template>

<script>
export default {
  name: 'ScoreButton',
  props: {
    score: Number
  },
  methods: {
    updateScore() {
      this.$emit('click', this.score)
    }
  },
  computed: {
    prefix() {
      return this.score >=0 ? '+' : '';
    },
    isNegative() {
      return this.score < 0;
    }
  }
}
</script>

<style scoped>
button {
  color: #42b983;
  border: 1px solid #42b983;
  margin: 0.5rem;
  padding: 0.2rem 0.5rem;
  border-radius: 5px;
  background-color: white;
  transition: all ease 0.5s;
  min-width: 4rem;
}

.negative {
  border-color: tomato;
  color: tomato;
}

button:hover {
  background-color: #42b983;
  color: white;
}

.negative:hover {
  background-color: tomato;
}
</style>

