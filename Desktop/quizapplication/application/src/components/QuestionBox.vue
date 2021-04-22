<template >
  <div>
    <b-jumbotron>
      <template #lead>
        {{ currentQuestion.question }}
      </template>
      <hr class="my-4" />
      <b-list-group v-for="(answer, index) in shuffledAnswers " :key="index">
        <b-list-group-item
          @click.prevent="selectAnswer(index)"
          :class="[selectIndex === index ? 'selected' : '']"
          >{{ answer }}</b-list-group-item
        >
      </b-list-group>
      <br />
      <b-button variant="warning" class="m-1" @click="previous" href="#"
        >Previous</b-button
      >
      <b-button variant="primary" class="m-1" @click="submitAnswer()" href="#"
        >Submit</b-button
      >
      <b-button variant="success" class="m-1" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
import _ from "lodash";
export default {
  name: "QuestionBox",
  props: {
    currentQuestion: Object,
    index: Number,
    next: Function,
    previous: Function,
    increment: Function
  },
  data() {
    return {
      selectIndex: null,
      correctIndex: null,
      shuffledAnswers: []
    };
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectIndex = null
        this.shuffleAnswer()
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectIndex = index;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectIndex === this.correctIndex) {
        isCorrect = true;
      }
      console.log(isCorrect);

      this.increment(isCorrect);
    },
    shuffleAnswer() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
  }
};
</script>
<style >
.list-group-item:hover {
  background-color: #f5f5f3;
}
.list-group-item.selected {
  background-color: lightblue;
  color: white;
}
b-jumbotron {
  font-family: "Poppins", sans-serif;
}
.list-group {
  font-family: "Poppins", sans-serif;
  font-weight: 500;
}
</style>