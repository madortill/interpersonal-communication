<template>
  <div id="app">
    <background class="back">

    </background>
  </div>
</template>

<script>
  import Background from './components/Background.vue';

  export default {
    name: "app",
    components: {
      Background
    },
    data() {
      return {
        
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

  .back {
    size: 100% 100%;
    width: 100vw;
    height: 100vh;
  }

  
</style>
