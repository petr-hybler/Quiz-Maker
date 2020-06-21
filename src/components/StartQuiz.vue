<template lang="html">
  <div class="container quiz">
      <div class="text-center">
         <button type="button" name="button" class="btn btn-primary" @click="start">Start</button>
      </div>
  </div>
</template>

<script>
import { Bus } from './../main.js';

export default {
  data() {
    return {

    }
  },
  methods: {
    start(){
      Bus.$emit('startQuiz');
    }
  }
}
</script>

<style lang="css" scoped>
</style>
