<template lang="html">
  <div class="container quiz">
    <transition name="fade" mode="out-in">

        <div v-if="isLastQuestion" key="result">
           <result :quizResult="quizResult"></result>
        </div>

        <div v-else key="question">
          <question :questionList="questionList"></question>
        </div>

    </transition>
  </div>
</template>

<script>
import Result from './Result.vue';
import Question from './Question.vue';

export default {
  props: ['questionList', 'isLastQuestion', 'quizResult'],
  components: {
    Result,
    Question,
  },
  data() {
    return {
    }
  },
  methods: {
  }
}
</script>

<style lang="css" scoped>
 .fade-enter {
   opacity: 0;
 }
 .fade-enter-active {
   transition: opacity 0.5s;
 }
 .fade-leave {

 }
 .fade-leave-active {
   transition: opacity 0.5s;
   opacity: 0;
 }
</style>
