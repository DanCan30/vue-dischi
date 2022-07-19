<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>

import Header from "./components/Header.vue";
import Main from "./components/Main.vue";


export default {

  components: {
    Header,
    Main,
  },

  }

</script>

<style lang="scss">
@import "./assets/stiles/common.scss";
@import "./assets/stiles/variables.scss";


div#app {
    font-family: 'Poppins', sans-serif;
    background-color: $bgColor;
    color: $textColor;
}
</style>
