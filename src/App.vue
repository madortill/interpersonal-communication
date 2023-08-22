<template>
  <div id="app">
    <nav-bar v-if="currSubj === 1" :currPage="currScreen" @change-page="changePage" class="nav-bar"></nav-bar>
    <main-content v-if="!(this.currScreen === 1 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)" 
      :currPage="currScreen" class="main-content"></main-content>
    <exercise-manager class="exercise-manager" v-if="(this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen === 21)" 
    :currPage="currScreen" @next-page="currScreen++"></exercise-manager>
  </div>
  <background id="background"></background>
  <img @click="currScreen++" class="arrow" src="@/assets/arrow-small-right.svg" alt="<--" 
  v-if="!(this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)">
</template>

<script>
  import Background from './components/Background.vue';
  import MainContent from './components/MainContent.vue';
  import NavBar from './components/NavBar.vue';
  import ExerciseManager from './components/ExerciseManager.vue';

  export default {
    name: "app",
    components: {
      Background,
      MainContent,
      NavBar,
      ExerciseManager
    },
    data() {
      return {
            currSubj: 0,
            currScreen: 1,
      }
    },
    methods: {
      changePage(page) {
        this.currScreen = page;
      }
    }
    
  }
</script>

<style>
  html,
  body {
    margin: 0;
    overflow: hidden;
    direction: rtl;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  html {
    font-size: calc(16px + 1vh);
    height: 100%;
  }

  #app {
    display: flex;
    position: relative;
    flex-wrap: wrap;
    align-content: center;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .main-content {
    width: 20rem;
    height: fit-content;
    position: relative;
    top: -2rem;
  }

  .arrow {
    width: 4rem;
    height: 4rem;
    position: absolute;
    bottom: 3rem;
    left: 3rem;
    rotate: 180deg;
  }

  .nav-bar {
    position: absolute;
    top: 27rem;
    left: 15rem;
  }

  #background {
    position: absolute;
    z-index: -1;
  }

  .exercise-manager {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    top: -2rem;
  }
</style>
