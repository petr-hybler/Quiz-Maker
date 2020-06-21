<template>
<div>
  <h1 style="text-align:center">Math Quiz</h1>
  <hr>
  <template v-if="quizRunning">
    <quiz :questionList="questionList[questionIdSelected]"
          :isLastQuestion="isLastQuestion"
          :quizStart="quizStart"
          :quizResult="testResults"
          ></quiz>
  </template>
  <template v-else>
    <start-quiz></start-quiz>
  </template>
</div>
</template>

<script>
import Quiz from './components/Quiz.vue';
import StartQuiz from './components/StartQuiz.vue';
import { Bus } from './main.js';

export default {
  data() {
    return {
      questionCount: 0,
      quizRunning: false,
      questionIdSelected: 0,
      isLastQuestion: false,
      testResults: {
            correct: 0,
            wrong: 0
      },
      questionList: [{
          id: 1,
          question: 'What is 5+6',
          answers: [{value: 5, correct: false},
                    {value: 29, correct: false},
                    {value: 15, correct: false},
                    {value: 11, correct: true}]
        },
        {
          id: 2,
          question: 'What is 20-8',
          answers: [{value: 18, correct: false},
                    {value: 28, correct: false},
                    {value: 12, correct: true},
                    {value: 6, correct: false}]
        },
        {
          id: 3,
          question: 'What is 11+9',
          answers: [{value: 13, correct: false},
                    {value: 8, correct: false},
                    {value: 19, correct: false},
                    {value: 20, correct: true}]
        },
      ],
    }
  },
  components: {
    Quiz,
    StartQuiz,
  },
  methods: {
    randomQuestionId() {
      var min = 1; // first element
      var max = this.questionList.length; // number of elements
      this.questionIdSelected = Math.floor(Math.random() * (max - min + 1)) + min -1;
    },
  },
  created() {
     Bus.$on('reset',() => {
         this.questionIdSelected = 0;
         this.quizRunning = false;
         this.isLastQuestion = false;
         this.testResults.correct = 0;
         this.testResults.wrong = 0;
     }),
     Bus.$on('startQuiz',() => {
         this.quizRunning = true;
     }),
     Bus.$on('sendAnswer',(answerResult, questionId) => {
         //store results
         answerResult == true ? this.testResults.correct++ : this.testResults.wrong++;

         //return next question
         if(this.questionIdSelected < this.questionList.length){
           this.questionIdSelected++;
         }
         if(this.questionIdSelected == this.questionList.length){
           this.isLastQuestion = true;
         }
     })
  }
}
</script>

<style>
.quiz {
  width: 60%;
}

.answerSheet {
  width: 80%;
  margin: 0 auto;
}

.answer {
  margin: 20px 0;
  width: 150px;
  padding: 5px 15px;
}
</style>
