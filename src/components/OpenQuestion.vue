<template>
  <div id="open-question">
      <div class="content-container">
        <span class="question">שאלה פתוחה:</span>
          <span class="question"> {{ ques.question }} </span>
          <textarea class="input" rows="4" cols="50" v-model="inputValue"></textarea>
          <span v-if="showEmpty && !checked" class="error-message">אופס, נראה שלא ענית על השאלה</span>
          <span v-if="checked" class="answer">
            <span>בדקו את עצמכם!</span>
            <br><span>תשובה: {{ ques.answer }} </span>
          </span>
          <button v-else class="check" @click="checkAnswer">אני רוצה לבדוק!</button>
          <button class="continue" v-show="checked" @click="proceed">הבנתי</button>
      </div>
  </div>
</template>

<script>
  
  export default {
    name: "open-question",
    props: ["ques"],
    data() {
      return {
          checked: false,
          showEmpty: false,
          inputValue: ''
      }
    },
    methods: {
      proceed() {
        this.inputValue = '';
        this.checked = false;
        this.$emit('finished');
      },
      checkAnswer() {
        if (!this.inputValue) {
          this.showEmpty = true;
        } else {
          this.showEmpty = false;
          this.checked = true;
        }
      }
    }
  }
</script>

<style scoped>
  .content-container {
    width: 100%;
    height: 100%;
    background-image: url("@/assets/background-text.svg");
    background-repeat: no-repeat;
    background-size: cover;
    padding: 10%;
    display: flex;
    flex-direction: column;
    width: 20rem;
  }

  .question, 
  .input,
  .answer,
  .check,
  /* .error-message, */
  .continue {
    margin: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .input {
    width: 80%;
    height: fit-content;
    resize: none;
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

  .error-message {
    font-size: 0.6rem;
    color: red;
    margin-right: 1rem;
  }

  .question,
  .answer {
    font-size: 0.7rem;
  }

</style>