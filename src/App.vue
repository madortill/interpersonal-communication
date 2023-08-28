<template>
  <div id="app">
    <nav-bar v-if="!(this.currScreen <= 3 || this.currScreen >= 21)" :currPage="currScreen" @change-page="changePage" class="nav-bar"></nav-bar>
    <open-end-screen :currPage="currScreen"></open-end-screen>
    <main-content v-if="!(this.currScreen <= 3 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)" 
      :currPage="currScreen" class="main-content"></main-content>
    <exercise-manager class="exercise-manager" v-if="(this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen === 21)" 
    :currPage="currScreen" @next-page="currScreen++"></exercise-manager>
  </div>
  <background id="background"></background>
  <img @click="currScreen++" class="arrow-forward" src="@/assets/arrow-white.svg" alt="<--" 
  v-if="!(this.currScreen === 1 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)">
  <img @click="currScreen--" class="arrow-back" src="@/assets/arrow-white.svg" alt="-->" 
  v-if="!(this.currScreen === 1 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)">
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
        currScreen: 4,
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
    width: 30rem;
    height: 17rem;
    position: relative;
    top: -5rem;
    right: -3rem;
  }

  .arrow-forward,
  .arrow-back {
    width: 4rem;
    height: 4rem;
    bottom: 3rem;
    position: absolute;
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
    top: -2rem;
    height: 20rem;
  }

  /* .main-content, 
  .exercise-manager {
    background-image: url("@/assets/background-text.svg");
    background-repeat: no-repeat;
    background-size: cover;
  } */
</style>
