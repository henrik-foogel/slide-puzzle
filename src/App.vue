<template>
  <div id="app">
    <Puzzle />
  </div>
</template>

<script>
import Puzzle from "./components/Puzzle.vue";

export default {
  name: "App",
  components: {
    Puzzle
  }
};
</script>

<style lang="scss">
body {
  background: #000;
}
#app {
  font-family: "Open Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
