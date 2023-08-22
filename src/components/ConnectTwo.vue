<template>
  <span class="question"> {{ ques.question }} </span>
  <div id="connect-two" class="content-container">
    <svg class="svg" viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg" ref="svg">
      <path :id="`path${index - 1}`" v-for="index in termsNum" :key="colorsArr[index - 1]" :stroke="colorsArr[index - 1]" stroke-width="0.5%" fill="none" :d="paths[index - 1]"></path>
    </svg>
    <div v-for="(string, keyName, index) in terms" :key="keyName" class="ignore">
      <div :class="['term', chosenTermIndex === index ? 'chosen' : '' ]" :style="`grid-column: ${index + 1} / ${index + 2}`" 
      @click="chosenTermIndex === index ? chosenTermIndex = -1 : chosenTermIndex = index"> {{ string }} </div>
      <div :class="['definition', chosenDefinitionIndex === index ? 'chosen' : '' ]" :id="`input${index}`" :style="`grid-column: ${index + 1} / ${index + 2}`" 
      @click="chosenDefinitionIndex === index ? chosenDefinitionIndex = -1 : chosenDefinitionIndex = index"> {{ Object.values(definitions)[index] }} </div>
    </div>
  </div>
  <span v-if="showEmpty && !checked" class="error-message">נראה שלא בחרת מושג והגדרה...</span>
  <button @click="checkConnection" class="connect">חבר</button>
</template>

<script>

  export default {
    name: "connect-two",
    props: ["ques"],
    emits: ['finished'],
    data() {
      return {
        terms: {},
        definitions: {},
        chosenTermIndex: -1,
        chosenDefinitionIndex: -1,
        termsNum: this.ques.term.length,
        colorsArr: ["#FFC0CB", "#03e3fc", "#d1043b", "#d16004", "#f57802", "#000000"],
        paths: [],
      }
    },
    mounted() {
      // fit SVG to screen proportions - take the CSS size of the svg element and set it to the viewBox values
      this.$refs.svg.setAttribute('viewBox', `0 0 ${this.$refs.svg.clientWidth} ${this.$refs.svg.clientHeight}`);

      for (let i = 0; i < this.ques.term.length; i++) {
        let random = Math.round(Math.random() * this.ques.term.length);
        while(`index${random}` in this.terms || random >= this.ques.term.length) {
          random = Math.round(Math.random() * this.ques.term.length);
        }
        this.terms[`index${random}`] = this.ques.term[random];
      }
      for (let j = 0; j < this.ques.definition.length; j++) {
        let random = Math.round(Math.random() * this.ques.definition.length);
        while(`index${random}` in this.definitions || random >= this.ques.definition.length) {
          random = Math.round(Math.random() * this.ques.definition.length);
        }
        this.definitions[`index${random}`] = this.ques.definition[random];
      }
    },
    methods: {
      checkConnection() {
        if (this.chosenTermIndex === -1 || this.chosenDefinitionIndex === -1) {
          alert ('לא נבחרו שני דברים לחיבור!')
        } else {
            
            let x1 = Number(this.chosenTermIndex) * (this.$refs.svg.clientWidth / this.termsNum) + (this.$refs.svg.clientWidth / this.termsNum / 2); 
            let x2 = Number(this.chosenDefinitionIndex) * (this.$refs.svg.clientWidth / this.termsNum) + (this.$refs.svg.clientWidth / this.termsNum / 2);
            let y1 = 0;
            let y2 = this.$refs.svg.clientHeight;   
            this.paths[this.chosenTermIndex] =  `M ${x1} ${y1} C ${x1} ${y2 * 1.2} ${x2} ${y2 * 0.01} ${x2} ${y2}`;
        }
      }
    },
  }
</script>

<style scoped>
  .content-container {
    width: 40rem;
    /* height: 100%; */
    height: 25rem;
    display: grid;
    grid-template: repeat(3, 1fr) / repeat(v-bind("termsNum"), 1fr);
    justify-items: center;
    direction: ltr;
  }

  .term,
  .definition {
    background-color: rgba(255, 255, 255, 0.589);
    border-radius: 0.5rem ;
    padding: 5%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 5rem;
    margin: 5%;
    text-align: center;
    justify-content: center;
  }

  .term:hover,
  .definition:hover {
    cursor: pointer;
  }

  
  .term {
    grid-row: 1 / 2;
    align-self: flex-end;
  }
  
  .definition {
    grid-row: 3/4;
    align-self: flex-start;
  }

  .svg {
    grid-column: 1 / -1;
    grid-row: 2 / 3;
    background-color: rgba(55, 238, 238, 0.422);
    width: 100%;
    height: 100%;
  }

  .ignore {
    display: contents;
  }

  .chosen {
    background-color: rgb(179, 238, 220);
  }

  .connect {
    position: absolute;
    bottom: 1rem;
  }

  .connect:hover {
    cursor: pointer;
  }

  .error-message {
    font-size: 0.6rem;
    color: red;
    margin-right: 1rem;
  }

</style>