<template>
  <div id="drag-and-drop" class="content-container">
    <!-- <div v-for="(string, keyName, index) in terms" :key="keyName">
      <div class="term"> {{ string }} </div>
      <div class="definition" :id="`input${index}`"> {{ Object.values(definitions)[index] }} </div>
    </div>
    <button @click="checkConnection" class="connect">חבר</button> -->
    <span class="question">גררו את ההגדרה למושג המתאים לה</span>
    <div class="draggable-container">
      <p v-for="(d, keyNameD, indexD) in definitions" :key="keyNameD" class="draggable" draggable="true" @dragstart="drag" :id="`drag${indexD}`">{{ d }}</p>
    </div>
    <div class="droppable-container">
      <div v-for="(t, keyNameT, indexT) in terms" :key="keyNameT" :id="`box-droppable${indexT}`" class="box-droppable" @drop="drop" @dragover="allowDrop"><p>{{ t }}</p></div>
    </div>
    <p id="txtFinish" v-show="finished">מעולה! כל הכבוד!</p>
  </div>
</template>

<script>

  export default {
    name: "drag-and-drop",
    props: ["ques"],
    data() {
      return {
        terms: {},
        definitions: {},
        answered: {},
        finished: false
      }
    },
    mounted() {
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
      onDragging(ev){
        ev.dataTransfer.setData("text", ev.target.id);
      },
      allowDrop(ev) {
        ev.preventDefault();
      },
      drag(ev) {
        ev.dataTransfer.setData("text", ev.target.id);
      },
      drop(ev) {
        ev.preventDefault();
        let data = ev.dataTransfer.getData("text");
        ev.target.appendChild(document.getElementById(data));
        this.answered[ev.currentTarget.id] = data;
        if (Object.keys(this.answered).length === 4) {
          if(this.checkAnswers()) {
            this.finished = true;
            this.$emit("finished");
          }
        }
      },
      checkAnswers() {
        for (let i = 0 ; i < this.ques.term.length ; i++ ) {
          if (this.answered[`box-droppable${i}`] !== this.correct[`box-droppable${i}`]) {
            return false;
          }
        }
        return true;
      }
    },
  }
</script>

<style scoped>
  .content-container {
    width: 100%;
    height: 100%;
    padding: 10%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: repeat(2, 1fr);
    width: 40rem;
    height: 15rem;
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
  }

  .draggable, .box-droppable {
    width: 5rem;
    border: 0.05rem solid #aaaaaa;
    border-radius: 1rem;
    display: block;
    text-align: center;
    font-size: 0.7rem;
  }

  .draggable{
    color: black;
    background-color: white;
    padding: 1rem;
    margin: 0 0.3rem;
    height: 7rem;
  }

  .box-droppable {
    background-color: darkgrey;
    padding: 0%;
    margin: 0 1rem;
    height: 3rem;
  }
  .droppable-container{
    top: 10%;
  }

  .droppable-container, 
  .draggable-container {
    position: absolute;
    display: flex;
    flex-direction: row;
    justify-content: center;
    width: 80%;
    height: 15%;
  }

  .draggable-container {
    bottom: 7rem;
  }

</style>