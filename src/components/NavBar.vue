<template>
  <div id="nav-bar">
    <ul>
      <li v-for="(subject, index) in subjects" :key="index"> {{ subject }} </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: "nav-bar",
  props: ["pageNum"],
  data() {
      return{
        subjects: [""]
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
  

</style>
