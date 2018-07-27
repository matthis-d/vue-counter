<template>
  <form @submit.prevent="addScore">
    <label for="count">Points </label>
    <input type="number" name="count" v-model="scoreToAdd" />
    <input type="submit" value="Add" />
  </form>
</template>

<script>
export default {
  name: 'ScoreForm',
  data() {
    return {
      scoreToAdd: null,
    }
  },
  computed: {
    intScoreToAdd() {
      return parseInt(this.scoreToAdd, 10);
    }
  },
  methods: {
    addScore() {
      this.$emit('score-added', this.intScoreToAdd);
      this.scoreToAdd = null;
    }
  }
}
</script>

<style scoped>
input[type="number"] {
  padding: 0.2rem 0.5rem;
}

input[type="submit"] {
  color: #42b983;
  border: 1px solid #42b983;
  margin: 0.5rem;
  padding: 0.2rem 0.5rem;
  border-radius: 5px;
  background-color: white;
  transition: all ease 0.5s;
}

input[type="submit"]:hover {
  background-color: #42b983;
  color: white;
}
</style>


