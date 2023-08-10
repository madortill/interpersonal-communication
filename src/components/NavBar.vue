<template>
  <div id="nav-bar">
    <ol class="progress">
      <li @click="changeScreen(subj1)" :class="[currPage >= 4 && currPage <= 11 ? 'is-active' : '']"><span>מושגים בתקשורת</span></li>
      <li @click="changeScreen(subj2)" :class="[currPage >= 12 && currPage <= 16 ? 'is-active' : '']"><span>מודלים תקשורתיים</span></li>
      <li @click="changeScreen(subj3)" :class="[currPage >= 17 && currPage <= 19 ? 'is-active' : '']"><span>סיבות לרעשים תקשורתיים</span></li>
      <li @click="changeScreen(subj4)" :class="[currPage >= 20 && currPage <= 21 ? 'is-active' : '']"><span>פתרונות לרעשים תקשורתיים</span></li>
    </ol>
  </div>
</template>

<script>

export default {
  name: "nav-bar",
  props: ["currPage"],
  data() {
      return{
        subj1: 4,
        subj2: 12,
        subj3: 17,
        subj4: 20
      };
  },
  methods: {
    changeScreen(page) {
      this.$emit('change-page', page);
    }
  },
}
</script>
  
<style scoped>
  
  :root {
    --color-white: #fff;
    --color-black: #333;
    --color-gray: #75787b;
    --color-gray-light: #bbb;
    --color-gray-disabled: #e8e8e8;
  }

  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Open Sans', sans-serif;
    color: var(--color-black);
    direction: rtl;
  }

  .progress {
    display: flex;
    justify-content: space-between;
    list-style: none;
    margin: 0 0 1rem 0;
    width: 45rem;
  }

  .progress li {
    flex: 2;
    position: relative;
    padding: 0 0 14px 0;
    font-size: 0.7rem;
    line-height: 1.2;
    color: var(--color-black);
    font-weight: 600;
    white-space: nowrap;
    overflow: visible;
    min-width: 0;
    text-align: center;
    border-bottom: 2px solid var(--color-gray-disabled);
  }

  .progress li:first-child,
  .progress li:last-child {
    flex: 1;
  }

  .progress li:last-child {
    text-align: center;
  }

  .progress li::before {
    content: "";
    display: block;
    width: 8px;
    height: 8px;
    background-color: var(--color-gray-disabled);
    border-radius: 50%;
    border: 2px solid var(--color-white);
    position: absolute;
    left: calc(50% - 6px);
    bottom: -7px;
    z-index: 3;
    transition: all .2s ease-in-out;
  }

  .progress li:first-child::before {
    left: 0;
  }

  .progress li:last-child::before {
    right: 0;
    left: auto;
  }

  .progress span {
    transition: opacity .3s ease-in-out;
  }

  .progress li:not(.is-active) span {
    opacity: 0;
  }

  .progress .is-complete:not(:first-child)::after,
  .progress .is-active:not(:first-child)::after {
    content: "";
    display: block;
    width: 100%;
    position: absolute;
    bottom: -2px;
    left: -50%;
    z-index: 2;
    border-bottom: 2px solid var(--color-yellow);
  }

  .progress li:last-child span {
    width: 200%;
    display: inline-block;
    position: absolute;
    left: -100%;
  }

  .progress .is-complete:last-child::after,
  .progress .is-active:last-child::after {
    width: 200%;
    left: -100%;
  }

  .progress .is-complete::before {
    background-color: var(--color-yellow);
  }

  .progress .is-active::before,
  .progress li:hover::before,
  .progress .is-hovered::before {
    background-color: var(--color-white);
    border-color: var(--color-yellow);
  }

  .progress li:hover::before,
  .progress .is-hovered::before {
    transform: scale(1.33);
  }

  .progress li:hover span,
  .progress li.is-hovered span {
    opacity: 1;
    cursor: pointer;
  }


  .progress:hover li:not(:hover) span {
    opacity: 0;
  }

  .progress .has-changes {
    opacity: 1 !important;
  }

  .progress .has-changes::before {
    content: "";
    display: block;
    width: 8px;
    height: 8px;
    position: absolute;
    left: calc(50% - 4px);
    bottom: -20px;
  } 

  .progress li .is-active span {
    opacity: 1 !important;
  }
</style>
