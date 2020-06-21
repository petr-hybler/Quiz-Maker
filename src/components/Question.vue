<template lang="html">
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Question {{questionList.id}}</h3>
      </div>
      <div class="panel-body text-center">
        <div class="container answerSheet">
          <div class="row">
            <div class="">
              <h4><strong>{{questionList.question}}</strong></h4>
            </div>
            <div class="col-sm-6 center" v-for="answer in questionList.answers">
              <button type="button" name="button" class="btn btn-primary answer" @click="checkAnswer(answer.correct,questionList.id)">{{answer.value}}</button>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import { Bus } from './../main';
export default {
   props: ['questionList'],
   data(){
     return{
     }
   },
   methods: {
     checkAnswer(answer, questionId) {
       if (answer == true) {
          Bus.$emit('sendAnswer', answer, questionId);
       } else {
          Bus.$emit('sendAnswer', answer, questionId);
       }
     }
   },
}
</script>

<style lang="css" scoped>
</style>
