<template>
  <div id="complete-sentence" class="content-container">
    <span class="question"> השלימו את המשפט: </span>
    <div v-for="(string, index) in ques.texts" :key="string">
      <span class="text"> {{ string }} </span>
      <input class="input" v-if="index < ques.answers.length" :id="`input${index}`" type="text" v-model="userInput[index]">
      <img class="indication" v-if="showAnswers" :src="indicationScr(index)">
    </div>
    <div class="input-container" v-if="showContainer">
      <span>מאגר תשובות:</span>
      <br><span v-for="input in ques.answers" :key="input"> {{ input }}, </span>
    </div>
    <button v-if="!allCorrect" class="check" @click="checkAnswers">בדוק אותי!</button>
    <button v-if="allCorrect" class="check" @click="proceed">בואו נמשיך!</button>
  </div>
</template>

<script>

  export default {
    name: "complete-sentence",
    props: ["ques"],
    data() {
      return {
        userInput: [],
        showAnswers: false,
        answerStatus: [],
        showContainer: false,
        timesAnswered: 0,
        allCorrect: false
      }
    },
    methods: {
      checkAnswers() {
        for (let index = 0; index < this.ques.answers.length; index++) {
          if (this.userInput[index] !== this.ques.answers[index]) {
            this.allCorrect = false;
            this.answerStatus[index] = "wrong";
          } else {
            this.allCorrect = true;
            this.answerStatus[index] = "correct";
          }
        }
        this.timesAnswered++;
        this.timesAnswered >= 3 ? this.showContainer = true : this.showContainer = false;
        this.showAnswers = true;
      },
      indicationScr(param) {
        if (this.answerStatus[param] === "correct") {
          return new URL("@/assets/correct.png", import.meta.url).href;
        } else {
          return new URL("@/assets/false.png", import.meta.url).href;
        }
      },
      proceed() {
        this.userInput = [];
        this.showAnswers = false;
        this.answerStatus = [];
        this.showContainer = false;
        this.timesAnswered = 0;
        this.$emit('finished');
      },
    }
  }
</script>

<style scoped>
  .content-container {
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.589);
    border-radius: 2rem;
    padding: 10%;
    display: flex;
    flex-direction: column;
    width: 20rem;
  }

  .check {
    margin: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 3rem;
    border: 0.06rem solid black;
    width: fit-content;
    align-self: center;
    font-weight: 500;
    font-size: 0.6rem;
    background-color: rgba(255, 255, 255, 0.5);
  }

  .input {
    width: 30%;
    height: fit-content;
    resize: none;
    font-size: 0.7rem;
  }

  .text, .input-container {
    font-size: 0.8rem;
  }

  .indication {
    width: 1rem;
  }

</style>