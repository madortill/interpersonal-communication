<template>
  <div id="multiple-choice">
    <div class="content-container">
      <!-- <span class="question"> {{ ques.quest }} </span>
      <div class="answers">
        <ul style="padding-right: 0; margin: 0;">
          <li v-for="(answer, index) in ques.ans" :key="index" class="ans" @click="revealAnswers(index)">
            <img class="indication" v-show="showAnswers && (index === ques.correct || index === chosenAnswer)" :src="indicationScr(index)">
            <span>{{ answer }}</span>
          </li>
        </ul>
        <button v-if="!showAnswers" class="check" @click="checkAnswers">יש לי את זה!</button>
        <button class="continue" v-show="showAnswers" @click="proceed">הבנתי!</button>
      </div> -->
      <span class="question"> {{ ques.quest }} </span>
      <br> <span class="question"> בחרו את התשובה הנכונה! </span>
      <div class="answers">
        <ul style="padding-right: 0; margin: 0;">
          <li v-for="(answer, index) in ques.ans" :key="index" :class="[index === chosenAnswer ? 'selected' : '', 'ans']" @click="selectAnswer(index)">
            <img class="indication" v-show="showAnswers && (index === ques.correct || index === chosenAnswer)" :src="indicationScr(index)">
            <span>{{ answer }}</span>
          </li>
        </ul>
      </div>
      <button v-if="!showAnswers" class="check" @click="checkAnswers">בדוק אותי!</button>
      <button class="continue" v-show="showAnswers" @click="proceed">בואו נמשיך</button>
    </div>
  </div>
</template>

<script>

  export default {
    name: "multiple-choice",
    props: ["ques"],
    data() {
      return {
        answerWrong: false,
        chosenAnswer: -1,
        showAnswers: false
      }
    },
    methods: {
      proceed() {
        this.chosenAnswer =  -1;
        this.$emit('finished');
      },
      indicationScr(param) {
        if (param === this.ques.correct) {
          return new URL("@/assets/correct.png", import.meta.url).href;
        } else {
          return new URL("@/assets/false.png", import.meta.url).href;
        }
      },
      selectAnswer(num) {
        this.chosenAnswer = num;
      },
      checkAnswers() {
        
      }
    }
  }
</script>

<style scoped>
  .content-container {
    width: 30rem;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.589);
    border-radius: 2rem;
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

  .question,
  .ans {
    font-size: 0.8rem;
  }

  .ans:hover {
    cursor: pointer;
     
  }

  .answers {
    display: flex;
  }

  .imgs {
    display: flex;
    list-style: none;
    margin-bottom: 1rem;
  }

  .selected {
    border: 0.1rem solid white;
  }

  .check,
  .continue {
    border-radius: 3rem;
    border: 0.06rem solid black;
    width: fit-content;
    align-self: center;
    font-weight: 500;
    font-size: 0.6rem;
    background-color: rgba(255, 255, 255, 0.5);
  }
  
</style>