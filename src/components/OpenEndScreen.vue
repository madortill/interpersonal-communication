<template>
  <div id="open-end-screen">
    <div class="open">
      <!-- start page -->
      <div v-if="currPage === 1" class="opening-container">
        <h1 class="start-header">תקשורת בין אישית</h1>
        <button class="start-btn" @click="nextPage">התחל</button>
      </div>

      <!-- animations -->
      <img v-show="showWave1" src="@/assets/comm-wave-3.svg" alt="comm-wave" class="comm-wave-large right">
      <img v-show="showWave2" src="@/assets/comm-wave-2.svg" alt="comm-wave" class="comm-wave-mid right">
      <img v-show="showWave3" src="@/assets/comm-wave-1.svg" alt="comm-wave" class="comm-wave-small right">
      <img v-show="showWave4" src="@/assets/comm-wave-6.svg" alt="comm-wave" class="comm-wave-small left">
      <img v-show="showWave5" src="@/assets/comm-wave-5.svg" alt="comm-wave" class="comm-wave-mid left">
      <img v-show="showWave6" src="@/assets/comm-wave-4.svg" alt="comm-wave" class="comm-wave-large left">

      <!-- main text -->
      <div class="text-container">
        <p v-show="showText" id="text" class="text">{{ text }}</p>
        <button class="general-btn" v-if="currPage === 2" @click="nextPage">אני רוצה לעזור!</button>
        <button class="general-btn" v-if="currPage === 3" @click="nextPage">בואו נתחיל!</button>
      </div>


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
      showRetry: false,

    }
  },
  mounted() {
    this.waveAnimation();
  },
  methods: {
    nextPage() {
      this.$emit('next-page');
    },
    waveAnimation() {
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
                            // this.$emit('next-page');
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
    }
  },
  computed: {
    text() {
      if (this.currPage <= 2) {
        return (json["Open"][0]);
      } else {
        return (json["End"][0]);
      }
    },
    showText() {
      if (this.showRetry && this.currPage === 21 || this.currPage === 1 || this.currPage === 0) {
        return false;
      } else {
        return true;
      }
    }
  },
  watch: {
    currPage: function () {
      this.waveAnimation();
    }
  }
}
</script>

<style scoped>
.open {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: flex-start;
  justify-content: center;
  align-items: center;
}

.opening-container {
  width: 100%;
  height: 100%;
  display: flex;
  align-content: center;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  flex-direction: column;
}

.text-container {
  width: 100%;
  height: 60%;
  display: flex;
  justify-content: center;
  justify-content: flex-start;
    align-items: center;
    padding-top: 3rem;
    flex-direction: column;
    align-content: center;

}

.start-btn {
  position: relative;
  z-index: 3;
  font-size: 1.2rem;
  font-family: assistant;
  padding: 0.2rem 1rem;
  border-radius: 30px;
  border: none;
  background-color: rgb(255, 255, 255);
}

.comm-wave-small {
  width: 2.2rem;
  height: 2.2rem;
}

.start-header {
  color: #f6f6f6;
  font-size: 5rem;
  width: 70%;
  text-align: center;
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
  text-align: center;
  width: 60%;
  color: rgb(28 32 45);
  font-size: 1.5rem;
}

/* button {
  position: relative;
  z-index: 3;
  margin: 1rem;
  font-family: assistant;
  border-radius: 3rem;
  border: 0.06rem solid rgb(255, 255, 255);
  width: 5rem;
  align-self: center;
  font-weight: 500;
  font-size: 0.6rem;
  background-color: rgb(0, 0, 0);
  color: white;
} */

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
  