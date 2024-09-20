<template>
  <div id="app" class="quiz-container">
    <h1>World Capitals Quiz</h1>
    <div v-if="question">
      <p><strong>Question:</strong> What is the capital of {{ question.country }}?</p>
      <input v-model="userAnswer" placeholder="Type your answer" />
      <button @click="checkAnswer">Submit</button>
    </div>

    <div v-if="feedback">
      <p>{{ feedback }}</p>
      <button @click="nextQuestion">Next Question</button>
    </div>

    <div class="scoreboard">
      <p><strong>Score:</strong> {{ score }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      countries: [
        { country: "Canada", capital: "Ottawa" },
        { country: "Australia", capital: "Canberra" },
        { country: "Japan", capital: "Tokyo" },
        { country: "Brazil", capital: "Brasília" },
        { country: "South Africa", capital: "Pretoria" }, // South Africa has 3 capitals, but this can be simplified for the quiz.
      ],
      question: null,
      userAnswer: "",
      feedback: "",
      score: 0,
    };
  },
  methods: {
    getRandomQuestion() {
      const randomIndex = Math.floor(Math.random() * this.countries.length);
      this.question = this.countries[randomIndex];
      this.userAnswer = "";
      this.feedback = "";
    },
    checkAnswer() {
      if (this.userAnswer.toLowerCase() === this.question.capital.toLowerCase()) {
        this.feedback = "Correct!";
        this.score++;
      } else {
        this.feedback = `Incorrect! The capital of ${this.question.country} is ${this.question.capital}.`;
      }
    },
    nextQuestion() {
      this.getRandomQuestion();
    },
  },
  mounted() {
    this.getRandomQuestion();
  },
};
</script>

<style scoped>
.quiz-container {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

input {
  margin-right: 10px;
}

.scoreboard {
  margin-top: 20px;
}
</style>
