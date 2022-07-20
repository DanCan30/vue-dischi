<template>
  <header>
    <img src="../assets/img/Spotify-logo.png" alt="Spotify Logo" id="logo">
  </header>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
@import "../assets/stiles/variables.scss";


    header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      background-color: $containersColor;
      height: 6vh;

        img#logo {
            max-width: 3rem;
            margin-left: 2rem;
            padding: 1rem 0;
        }
    }

</style>