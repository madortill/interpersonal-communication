<template>
  <div id="background">
    <div class="background">
      <img src="@/assets/communication-towers.svg" alt="communication-towers" style="position: absolute; bottom: -4rem;">
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
    height: 100vh;
    width: 100vw;
    background-image: url("@/assets/background-day.svg");
    background-size: cover;
    background-repeat: no-repeat;
    position: relative;
  }

</style>
  