<template>
    <div id="multiple-choice-answer">
        <div class="answers">
            <img v-show="showCorrect" class="indication" src="@/assets/correct.png" alt="V"><img v-show="showFalse" class="indication" src="@/assets/false.png" alt="X">
            <span @click="checkAnswer"> {{ text }} </span>
        </div>
    </div>
</template>
  
<script>
  
    export default {
      name: "multiple-choice-answer",
      props: ["text", "param", "corrAns", "answeredWrongly"],
      data() {
        return {
          showCorrect: false,
          showFalse: false,
          answerStatus: ''
        }
      },
      methods: {
        checkAnswer() {
            if (this.param === this.corrAns) {
                this.showCorrect = true;
                this.answerStatus = 'correct'; 
            } else {
                this.showFalse = true;
                this.answerStatus = 'false';
            }
            this.$emit('answered', this.answerStatus);
        }
      },
      computed: {
        showCorrectAns() {

        }
      }
    }
</script>
  
<style scoped>
    .indication {
        width: 1rem;
    }

    .ans {
        list-style: none;
        margin: 0.7rem;
    }

    .answers {
        display: flex;
    }

    .imgs {
        display: flex;
        list-style: none;
        margin-bottom: 1rem;
    }
  
</style>