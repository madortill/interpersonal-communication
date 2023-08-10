<template>
    <div id="open-question">
        <div class="content-container">
            <span class="question"> {{ question }} </span>
            <input type="text">
            <span v-if="checked" class="answer"> {{ answer }} </span>
            <button v-else class="check" @click="showAnswer">בדוק אותי!</button>
            <button v-show="checked" @click="proceed">המשך</button>
        </div>
    </div>
  </template>
  
  <script>
  import json from '@/data.json'
  
    export default {
      name: "open-question",
      components: {
        
      },
      data() {
        return {
            question: "what is the color blue?",
            answer: "the color blue is blue",
            checked: false,
        }
      },
      methods: {
        proceed() {
            this.$emit('finished');
        }
      }
    }
  </script>
  
  <style scoped>
    .content-container {
        width: 100%;
        height: 100%;
        background-color: rgba(255, 255, 255, 0.589);
        border-radius: 20%;
        padding: 10%;
    }
  
  </style>