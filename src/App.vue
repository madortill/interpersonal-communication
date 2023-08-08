<template>
  <background class="back"></background>
  <main-content v-show="!(this.currScreen === 1 || this.currScreen === 11 || this.currScreen === 16 || this.currScreen === 19 || this.currScreen === 21)" :currScreen="currScreen" class="main-content"></main-content>
  <img @click="currScreen++" class="arrow" src="@/assets/arrow-small-right.svg" alt="<--">
</template>

<script>
  import Background from './components/Background.vue';
  import MainContent from './components/MainContent.vue';

  export default {
    name: "app",
    components: {
      Background,
      MainContent
    },
    data() {
      return {
        subj: ["Algorithm", "Complex", "OrderOfMagnitude"],
            currSubj: 0,
            currScreen: 1,
      }
    },
    methods: {
      
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
</style>
