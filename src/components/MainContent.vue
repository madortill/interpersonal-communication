<template>
  <div id="main-content">
    <div class="content-container">
      <p id="title" class="titles">{{ title[currSubj] }}</p>
      <div class="content">
        <p v-for="(t, index) in content[`page${currPage}`]" :key="index">{{ t }}</p>
      </div>
    </div>
  </div>
</template>
  
<script>
import json from '@/data.json'

  export default {
    name: "main-content",
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
          if (this.currPage === 3) {
            num = 0;
          } else if (this.currPage === 4) {
            num = 1;
          } else if (this.currPage >= 5 && this.currPage < 10) {
            num = 2;
          } else if (this.currPage === 11) {
            num = 3;
          } else if (this.currPage >= 12 && this.currPage < 14) {
            num = 4;
          } else if (this.currPage === 14) {
            num = 5;
          } else if (this.currPage >= 15) {
            num = 6;
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
    position: relative;
    /* right: 2rem; */
    top: -1rem;

  }

  .titles {
    font-weight: 600;
  }

  .content, 
  .titles {
    position: relative;
    top: -2rem;
  }

</style>
