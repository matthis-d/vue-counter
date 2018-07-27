<template>
  <div class="hello">
    <h1>Score counter</h1>
    <div class="form">
      <ScoreForm @score-added="updateScore($event)" />
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

import ScoreButton from './ScoreButton';
import ScoreForm from './ScoreForm';

export default {
  name: "HelloWorld",
  components: {
    ScoreButton,
    ScoreForm,
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
</style>
