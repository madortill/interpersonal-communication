<template>
  <div id="app">
    <open-end-screen v-if="currScreen <= 2 || currScreen === 21" @next-page="currScreen++" :currPage="currScreen"></open-end-screen>
    <main-content v-if="!(this.currScreen <= 2 || this.currScreen === 10 || this.currScreen === 15 || this.currScreen === 18 || this.currScreen >= 20)" 
      :currPage="currScreen" class="main-content"></main-content>
    <exercise-manager class="exercise-manager" v-if="(this.currScreen === 10 || this.currScreen === 15 || this.currScreen === 18 || this.currScreen === 20)" 
      :currPage="currScreen" @next-page="currScreen++"></exercise-manager>
  </div>
  <background id="background"></background>
  <img v-show="currScreen >= 2 && currScreen <= 21" src="@/assets/background-text.svg" alt="background-text" class="bg-text">
  <img src="@/assets/communication-towers.svg" alt="communication-towers" style="position: absolute; bottom: -6rem; width: 70rem; height: 48rem;">
  <nav-bar v-if="!(this.currScreen <= 2 || this.currScreen > 20)" :currPage="currScreen" @change-page="changePage" class="nav-bar"></nav-bar>
  <img @click="currScreen++" class="arrow-forward" src="@/assets/arrow-white.svg" alt="<--" 
  v-if="!(this.currScreen <= 2 || this.currScreen === 10 || this.currScreen === 15 || this.currScreen === 18 || this.currScreen >= 20)">
  <img @click="currScreen--" class="arrow-back" src="@/assets/arrow-white.svg" alt="-->" 
  v-if="!(this.currScreen <= 2 || this.currScreen === 10 || this.currScreen === 15 || this.currScreen === 18 || this.currScreen >= 20)">
</template>

<script>
  import Background from './components/Background.vue';
  import MainContent from './components/MainContent.vue';
  import NavBar from './components/NavBar.vue';
  import ExerciseManager from './components/ExerciseManager.vue';
  import OpenEndScreen from './components/OpenEndScreen.vue';

  export default {
    name: "app",
    components: {
      Background,
      OpenEndScreen,
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
    font-size: calc(16px + 0.7vw);
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
    width: 28rem;
    height: 17rem;
    position: relative;
  }

  .bg-text {
    width: 33rem;
    height: 23rem;
    position: absolute;
    top: 3.5rem;
    z-index: -1;
  }

  .arrow-forward,
  .arrow-back {
    width: 4rem;
    height: 4rem;
    bottom: 3rem;
    position: absolute;
  }

  .arrow-forward:hover,
  .arrow-back:hover {
    cursor: pointer;
  }

  .arrow-forward {
    rotate: 180deg;
    left: 0.5rem;
  }

  .arrow-back {
    right: 0.5rem;
  }

  .nav-bar {
    position: absolute;
    top: 27rem;
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
    top: -1rem;
    right: -2rem;
    height: 22rem;
    z-index: 2;
  }

  /* .main-content, 
  .exercise-manager {
    background-image: url("@/assets/background-text.svg");
    background-repeat: no-repeat;
    background-size: cover;
  } */
</style>
