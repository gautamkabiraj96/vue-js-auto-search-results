<template>
  <div id="app">
    <AutoSearch />
  </div>
</template>

<script>
import AutoSearch from "./components/AutoSearch";

export default {
  name: "App",
  components: {
    AutoSearch,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
