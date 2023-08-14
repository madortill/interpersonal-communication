<template>
  <div id="exercise-manager">
    <div>
      <open-question v-if="currSubj === 1" class="open-question"></open-question>
      <multiple-choice :ques="ques1"></multiple-choice>
    </div>
  </div>
</template>

<script>
  import OpenQuestion from './OpenQuestion.vue';
  import MultipleChoice from './MultipleChoice.vue';

  export default {
    name: "exercise-manager",
    components: {
      OpenQuestion,
      MultipleChoice
    },
    data() {
      return {
        currSubj: 0,
        ques1: {
          quest: "לוחם לא ענה לחברה שלו לשיחה מכיוון שהיה בפעילות מבצעית, החברה הסיקה שלא אכפת לו כבר ממנה. מה המקור של ה'רעש' התקשורתי במקרה הזה?",
          ans: {
            ans1: "בעיה בהצפנה",
            ans2: "בעיה בבחירת ערוץ או אמצעי תקשורת",
            ans3: "בעיה בקליטה של המסר",
            ans4: "בעיה בפענוח",
          },
          correct: "ans4"
        }
      }
    },
    methods: {
      
    }
  }
</script>

<style scoped>
  

</style>
