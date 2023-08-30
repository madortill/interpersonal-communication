<template>
  <div id="complete-sentence" class="content-container">
    <span class="question"> השלימו את המשפט: </span>
    <div v-for="(string, index) in ques.texts" :key="string">
      <span class="text"> {{ string }} </span>
      <input class="input" v-if="index < ques.answers.length" :id="`input${index}`" type="text" v-model="userInput[index]">
      <img class="indication" v-if="showAnswers && answerStatus[index] !== 'null'" :src="indicationScr(index)">
    </div>
    <div class="input-container" v-if="showContainer">
      <span>היעזרו במאגר המילים:</span>
      <div v-for="input in ques.answers" :key="input" class="item">
        <br><span> {{ input }} </span>
      </div>
    </div>
    <button v-if="!allCorrect" class="check" @click="checkAnswers">בדוק אותי!</button>
    <button v-if="allCorrect" class="check" style="width: 5rem;" @click="proceed">בואו נמשיך!</button>
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
        for (let index = 0; index < this.ques.texts.length; index++) {
          if (this.userInput[index] === undefined) {
            this.answerStatus[index] = "null";
          } else if (this.userInput[index] === this.ques.answers[index]) {
            this.answerStatus[index] = "correct";
          } else {
            this.answerStatus[index] = "wrong";
          }
        }
        this.allCorrect = true;
        for (let i = 0; i < this.answerStatus.length; i++) {
          if (this.answerStatus[i] === "wrong") {
            this.allCorrect = false;
          }
        }
        this.timesAnswered++;
        this.timesAnswered >= 3 ? this.showContainer = true : this.showContainer = false;
        this.showAnswers = true;
      },
      indicationScr(param) {
        if (this.answerStatus[param] === "correct") {
          return new URL("@/assets/correct.svg", import.meta.url).href;
        } else {
          return new URL("@/assets/wrong.svg", import.meta.url).href;
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
    height: 12rem;
    padding: 10%;
    display: flex;
    flex-direction: column;
    width: 20rem;
  }

  .question {
    font-size: 0.9rem;
  }

  .check {
    margin: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 3rem;
    border: 0.06rem solid rgb(255, 255, 255);
    width: 4rem;
    align-self: center;
    font-weight: 500;
    font-size: 0.6rem;
    background-color: rgb(0, 0, 0);
    color: white;
    position: relative;
    right: -2rem;
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

  .input-container {
    border: 0.1rem solid black;
    padding: 0.4rem;
    border-radius: 1rem;
    margin-top: 1rem;
    align-self: center;
    text-align: center;
    width: 10rem;
    position: relative;
    right: -2rem;
  }

  .indication {
    width: 1rem;
    margin: 0 0.2rem;
  }

  .item {
    line-height: 0.6rem;
  }

  button:hover {
    cursor: pointer;
  }

</style>