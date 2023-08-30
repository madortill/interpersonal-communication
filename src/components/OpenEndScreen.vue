<template>
  <div id="open-end-screen">
    <div class="open">
      <img v-show="showWave1" src="@/assets/comm-wave-3.svg" alt="comm-wave" class="comm-wave-large right">
      <img v-show="showWave2" src="@/assets/comm-wave-2.svg" alt="comm-wave" class="comm-wave-mid right">
      <img v-show="showWave3" src="@/assets/comm-wave-1.svg" alt="comm-wave" class="comm-wave-small right">
      <img v-show="showWave4" src="@/assets/comm-wave-6.svg" alt="comm-wave" class="comm-wave-small left">
      <img v-show="showWave5" src="@/assets/comm-wave-5.svg" alt="comm-wave" class="comm-wave-mid left">
      <img v-show="showWave6" src="@/assets/comm-wave-4.svg" alt="comm-wave" class="comm-wave-large left">
      <p v-show="showText" id="text" class="text">{{ text }}</p>
      <button v-if="currPage === 2" @click="nextPage">אני רוצה לעזור!</button>
      <button v-if="currPage === 3" @click="nextPage">בואו נתחיל!</button>
      <div v-if="currPage === 21 && showRetry === true" class="retry">
        <img src="@/assets/re-do-icon.svg" alt="redo" style="width: 3rem; margin-right: 0.5rem; margin-bottom: 1rem;">
        <span>באלי שוב!</span>
      </div>
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
        showWave1: false,
        showWave2: false,
        showWave3: false,
        showWave4: false,
        showWave5: false,
        showWave6: false,
        showRetry: false
      }
    },
    mounted() {
      if (this.currPage === 1 || this.currPage === 21) {
        setTimeout(() => {
          this.showWave3 = true;
          setTimeout(() => {
            this.showWave2 = true;
            setTimeout(() => {
              this.showWave1 = true;
              setTimeout(() => {
                this.showWave1 = false;
                this.showWave2 = false;
                this.showWave3 = false;
                setTimeout(() => {
                  this.showWave4 = true;
                  setTimeout(() => {
                    this.showWave5 = true;
                    setTimeout(() => {
                      this.showWave6 = true;
                      setTimeout(() => {
                        this.showWave4 = false;
                        this.showWave5 = false;
                        this.showWave6 = false;
                        setTimeout(() => {
                          if (this.currPage === 21) {
                            this.showRetry = true;
                          } else {
                            this.$emit('next-page');
                          }
                        }, 500);
                      }, 500);
                    }, 500);
                  }, 500);
                }, 500);
              }, 500);
            }, 500);
          }, 500);
        }, 500);
      }
    },
    methods: {
      nextPage() {
        this.$emit('next-page');
      },
      showText() {
        if (this.showRetry && this.currPage === 21 || this.currPage === 1) {
          return false;
        } else {
          return true;
        }
      }
    },
    computed: {
      text() {
        if (this.currPage <= 2) {
          return (json["Open"][0]);
        } else {
          return (json["End"][0]);
        }
      }
    },
    watch: {
      currPage: function () {
        if (this.currPage === 1 || this.currPage === 21) {
          setTimeout(() => {
            this.showWave3 = true;
            setTimeout(() => {
              this.showWave2 = true;
              setTimeout(() => {
                this.showWave1 = true;
                setTimeout(() => {
                  this.showWave1 = false;
                  this.showWave2 = false;
                  this.showWave3 = false;
                  setTimeout(() => {
                    this.showWave4 = true;
                    setTimeout(() => {
                      this.showWave5 = true;
                      setTimeout(() => {
                        this.showWave6 = true;
                        setTimeout(() => {
                          this.showWave4 = false;
                          this.showWave5 = false;
                          this.showWave6 = false;
                          setTimeout(() => {
                            this.showRetry = true;
                          }, 500);
                        }, 500);
                      }, 500);
                    }, 500);
                  }, 500);
                }, 500);
              }, 500);
            }, 500);
          }, 500);
        }
      }
    }
  }
</script>

<style scoped>
  
  .open {
    width: 100%;
    height: 100%;
    padding: 10%;
  }

  .comm-wave-small {
    width: 2.2rem;
    height: 2.2rem;
  }

  .comm-wave-mid {
    width: 4rem;
    height: 4rem;
  }

  .comm-wave-large {
    width: 6.5rem;
    height: 6.5rem;
  }

  .comm-wave-large,
  .comm-wave-mid,
  .comm-wave-small {
    position: absolute;
  }

  .left {
    left: 32rem;
    bottom: 15rem;
    rotate: -10deg;
  }

  .right {
    right: 32rem;
    bottom: 15rem;
    rotate: 10deg;
  }

  .comm-wave-large.right {
    right: 26.5rem;
  }

  .comm-wave-mid.right {
    right: 29.5rem;
  }

  .comm-wave-large.left {
    left: 26.5rem;
  }

  .comm-wave-mid.left {
    left: 29.5rem;
  }

  .text {
    width: 28rem;
    height: 17rem;
    position: relative;
    left: 3rem;
    top: 3rem;
    text-align: center;
  }

  button:hover {
    cursor: pointer;
  }

  button {
    position: relative;
    z-index: 3;
    margin: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 3rem;
    border: 0.06rem solid rgb(255, 255, 255);
    width: 5rem;
    align-self: center;
    font-weight: 500;
    font-size: 0.6rem;
    background-color: rgb(0, 0, 0);
    position: relative;
    right: 7rem;
    bottom: 2rem;
    color: white;
  }

  .retry {
    display: flex;
    flex-direction: column;
    position: relative;
    bottom: 9rem;
    right: 9rem;
  }

  .retry :hover {
    cursor: pointer;
  }

</style>
  