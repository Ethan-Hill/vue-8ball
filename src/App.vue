<template>
  <div id="app">
    <h1>8 Ball Answer Provider</h1>
    <hr>
    <b-field>
      <b-input placeholder="Am I amazing?" size="is-large" v-model="question">
      </b-input>
    </b-field>
    
    <b-button type="is-success" @click="ask" outlined>Ask</b-button>
    <br>
    <h1 v-if="answer">{{ answer }}</h1>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      question: null,
      answer: null,
    };
  },
  methods: {
    ask() {
      this.answer = null;
      axios
        .get(`https://8ball.delegator.com/magic/JSON/${this.question}`)
        .then((response) => {
          this.question = null;
          this.answer = response.data.magic.answer;
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
  },
};
</script>

<style>
body {
  height: 100vh;
  background-color: #3f4041;
  display: flex;
  align-items: center;
  justify-content: center;
}

#app {
  width: 50vw;
  text-align: center;
  font-size: 60px;
  color: #fff;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
