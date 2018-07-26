<template>
  <div class="hello">
    <h1>Score counter</h1>
    <div class="form">
      <form @submit.prevent="computeScore">
        <label for="count">Points </label>
        <input type="number" name="count" v-model="scoreToAdd" />
        <input type="submit" value="Add" />
      </form>
    </div>
    <div class="quick-actions">
      <ScoreButton
        v-for="score in quickScores"
        :key="score"
        :score="score"
        @click="updateScore($event)"
      />
    </div>
    <div class="current-score">
      <h2>
        Score<br/>
        {{counter}}
      </h2>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import ScoreButton from './ScoreButton'

export default {
  name: "HelloWorld",
  components: {
    ScoreButton,
  },
  mounted() {
    axios
      .get('https://api.keyvalue.xyz/b05f2221/counter')
      .then(res => this.counter = parseInt(res.data, 10));
  },
  data() {
    return {
      counter: null,
      scoreToAdd: null,
      quickScores: [100, 200, 2000],
    };
  },
  methods: {
    updateScore(score) {
      this.counter = parseInt(this.counter, 10) + parseInt(score, 10);
      return axios
        .post('https://api.keyvalue.xyz/b05f2221/counter', this.counter)
        .then(res => this.score = res.data);
    },
    computeScore() {
      this.updateScore(parseInt(this.scoreToAdd, 10));
      this.scoreToAdd = null;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}

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
