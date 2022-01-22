<template>
  <div id="app">
    <h1>Let's go get drunk!</h1>
    <BeerForYou />
  </div>
</template>

<script>
import BeerForYou from "./components/BeerForYou.vue";

export default {
  name: "App",
  components: {
    BeerForYou,
  },
};
</script>

<style lang="scss">
body {
    background-color: #ebebeb;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // margin-top: 60px;
}
</style>
