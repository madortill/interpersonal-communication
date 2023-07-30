<template>
    <div id="background">
      <div class="background">
      </div>
    </div>
  </template>
  
  <script>
  
    export default {
      name: "background",
      components: {
        
      },
      data() {
        return {
          
        }
      },
      methods: {
        
      }
    }
  </script>
  
  <style scoped>
    
    .background {
        height: calc(var(--vh, 1vh) * 100);
        width: 100vw;
        /* background-image: url("@/assets/"); */
        background-color: rgb(3, 190, 223);
        background-size: 100vw 100vh;
        background-repeat: no-repeat;
    }

  </style>
  