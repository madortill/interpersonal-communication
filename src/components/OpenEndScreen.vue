<template>
  <div id="open-end-screen">
    <div class="open">
      <p id="text" class="text">{{ text[currpage - 2] }}</p>
    </div>
  </div>
</template>

<script>
  import json from '@/data.json';

  export default {
    name: "open-end-screen",
    props: ["currPage"],
    data() {
      return {
        towersAnimation: false,
        
      }
    },
    mounted() {
      setTimeout(() => {

      }, 3000);
    },
    methods: {
      
    },
    computed: {
      text() {
        return (json["Open"]);
      },
    }
  }
</script>

<style scoped>
  
  .open {
    width: 100%;
    height: 100%;
    background-image: url("@/assets/background-text.svg");
    background-repeat: no-repeat;
    background-size: cover;
    padding: 10%;
  }

</style>
  