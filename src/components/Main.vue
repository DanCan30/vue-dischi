<template>
  <main>
    <CardsContainer />
  </main>
</template>

<script>

import CardsContainer from "./CardsContainer.vue";

export default {

    components: {
        CardsContainer,
    }

}
</script>

<style lang="scss" scoped>

    main {
        height: 100vh;
        padding: 6vh 0;
    }
</style>