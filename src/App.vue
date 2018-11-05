<template>
  <div id="app">
    <SearchBar />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";

export default {
  name: "App",
  components: {
    SearchBar
  }
};
</script>

<style lang="less">
body {
  margin: 0;
  padding: 0;
  background-color: royalblue;
  min-width: 320px;
}

#app * {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  list-style-type: none;
}
</style>
