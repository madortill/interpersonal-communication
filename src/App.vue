<template>
  <background class="back"></background>
  <nav-bar v-if="currSubj === 1" :currPage="currScreen" @change-page="changePage" class="nav-bar"></nav-bar>
  <main-content v-if="currSubj === 1" v-show="!(this.currScreen === 1 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen >= 21)" :currPage="currScreen" class="main-content"></main-content>
  <open-question class="open-question"></open-question>
  <img @click="currScreen++" class="arrow" src="@/assets/arrow-small-right.svg" alt="<--">
</template>

<script>
  import Background from './components/Background.vue';
  import OpenQuestion from './components/OpenQuestion.vue';
  import MainContent from './components/MainContent.vue';
  import NavBar from './components/NavBar.vue';

  export default {
    name: "app",
    components: {
      Background,
      MainContent,
      NavBar,
      OpenQuestion
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

  .main-content {
    width: 20rem;
    height: fit-content;
    position: absolute;
    z-index: 5;
    top: 5rem;
    left: 50%;
    transform: translateX(-50%);

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

  .open-question {
    position: absolute;
    
  }
</style>
