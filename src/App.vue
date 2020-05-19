<template>
  <div id="app">
    <Home />
  </div>
</template>

<style lang="scss">
  body {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    background-image: url("assets/bg.jpg");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }
</style>
<script>
  import Home from "./views/Home";
  export default {
    components: {Home}
  }
</script>
