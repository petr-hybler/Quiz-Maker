<template lang="html">
    <div class="panel panel-success">
      <div class="panel-heading">
        <h1 style="text-align: center">Results!</h1>
      </div>
      <div class="panel-body bg-success text-center">
            <p>Correct answers: {{quizResult.correct}}</p>
            <p>Wrong answers: {{quizResult.wrong}}</p>
            <p>Ratio: {{ ((quizResult.correct / (quizResult.correct + quizResult.wrong)) *100).toFixed(1) }} %</p>
            <hr>
            <button type="button"
                    name="button"
                    class="btn btn-primary"
                    @click="reset"
                    >Done</button>
      </div>
    </div>
</template>

<script>
import { Bus } from './../main.js';

export default {
  props: ['quizResult'],
  data() {
    return {
    }
  },
  methods: {
    reset() {
      Bus.$emit('reset');
    }
  }
}
</script>

<style lang="css" scoped>
</style>
