<template>
  <div id="main-content">
    <div class="content-container">
      <p id="title" class="titles">{{ title[currSubj] }}</p>
      <div class="">
        <p v-for="(t, index) in content[`page${currPage}`]" :key="index">{{ t }}</p>
      </div>
    </div>
  </div>
</template>
  
<script>
import json from '@/data.json'

  export default {
    name: "main-content",
    components: {
      
    },
    props: ['currPage'],
    computed: {
        content() {
          return (json["Content"][0]);
        },
        title() {
          return (json["Title"]);
        },
        currSubj() {
          let num = '';
          if (this.currPage === 4) {
            num = 0;
            console.log("מהי תקשורת?");
          } else if (this.currPage === 5) {
            num = 1;
            console.log("איזו תקשורת קיימת בהדרכה?");
          } else if (this.currPage >= 6 && this.currPage < 11) {
            num = 2;
            console.log("מושגים בתקשורת");
          } else if (this.currPage === 12) {
            num = 3;
            console.log("תקשורת קווית");
          } else if (this.currPage >= 13 && this.currPage < 15) {
            num = 4;
            console.log("תקשורת מעגלית");
          } else if (this.currPage === 15) {
            num = 5;
            console.log("תקשורת בהדרכה");
          } else if (this.currPage >= 16) {
            num = 6;
            console.log("רעשים בתקשורת");
          }
          return num;
        }
    }
  }
</script>

<style scoped>
  .content-container {
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0.589);
    border-radius: 20%;
    padding: 10%;
  }

  .titles {

  }

</style>
