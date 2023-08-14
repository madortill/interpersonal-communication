<template>
  <div id="multiple-choice">
    <div class="content-container">
      <span class="question"> {{ ques.quest }} </span>
      <div class="answers">
        <ul style="padding-right: 0; margin: 0;">
          <li v-for="(answer, index) in ques.ans" :key="index" class="ans"><multiple-choice-answer @answered="proceed(answerStatus)" :text="answer" :answeredWrongly="answerWrong" :param="index" :corrAns="ques.correct">
          </multiple-choice-answer></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import MultipleChoiceAnswer from './MultipleChoiceAnswer.vue';

  export default {
    name: "multiple-choice",
    props: ["ques"],
    components: {
      MultipleChoiceAnswer
    },
    data() {
      return {
        answerWrong: false
      }
    },
    methods: {
      proceed(answerStatus) {
        setTimeout(() => {  
          if (answerStatus === 'correct'){
            this.$emit('finished');
          } else {
            this.answerWrong = true;
            setTimeout(() => {
              this.$emit('finished');
            } ,3000);
          }
          } ,1500);
      },
    },
  }
</script>

<style scoped>
  .content-container {
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.589);
    border-radius: 20%;
    padding: 10%;
    display: flex;
    flex-direction: column;
  }

  .indication {
    width: 1rem;
  }

  .ans {
    list-style: none;
    margin: 0.7rem;
  }

  /* .question {

  } */

  .answers {
    display: flex;
  }

  .imgs {
    display: flex;
    list-style: none;
    margin-bottom: 1rem;
  }
  
</style>