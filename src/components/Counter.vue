<template>
  <div class="hello">
    <h1>Score counter</h1>
    <div class="form">
      <form @submit.prevent="computeScore">
        <label for="count">Points </label>
        <input type="number" name="count" v-model="scoreToAdd" />
        <button>Add</button>
      </form>
    </div>
    <div class="quick-actions">
      <button @click="updateScore(100)">+100</button>
      <button @click="updateScore(200)">+200</button>
      <button @click="updateScore(2000)">+2000</button>
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

export default {
  name: "HelloWorld",
  mounted() {
    axios
      .get('https://api.keyvalue.xyz/b05f2221/counter')
      .then(res => this.counter = parseInt(res.data, 10));
  },
  data() {
    return {
      counter: null,
      scoreToAdd: 0
    };
  },
  methods: {
    updateScore(score) {
      this.counter += score;
      return axios
        .post('https://api.keyvalue.xyz/b05f2221/counter', this.counter)
        .then(res => this.score = res.data);
    },
    computeScore() {
      this.updateScore(parseInt(this.scoreToAdd, 10));
      this.scoreToAdd = 0;
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

button {
  color: #42b983;
  border: 1px solid #42b983;
  margin: 0.5rem;
  padding: 0.2rem 0.5rem;
  border-radius: 5px;
}

button:hover {
  background-color: #42b983;
  color: white;
}
</style>
