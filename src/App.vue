<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
  export default {
    name: 'app'
  }
</script>

<style lang="scss">
  @import '../node_modules/bootstrap/scss/bootstrap';
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,400i,700');

  #app {
    background-color: silver;
    background-image: linear-gradient(335deg, #b00 23px, transparent 23px),
    linear-gradient(155deg, #d00 23px, transparent 23px),
    linear-gradient(335deg, #b00 23px, transparent 23px),
    linear-gradient(155deg, #d00 23px, transparent 23px);
    background-size: 58px 58px;
    background-position: 0px 2px, 4px 35px, 29px 31px, 34px 6px;

    font-family: 'Montserrat', sans-serif;
    color: #2c3e50;
  }
</style>
