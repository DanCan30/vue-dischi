<template>
  
    <div class="disk">

        <div class="img-container">
            <img :src="poster" :alt="`${title} performed by ${author}`">
        </div>

        <h2>{{ title }}</h2>
        <p>{{ author }}</p>
        <p>{{ year }}</p>

    </div>

</template>

<script>
export default {

    props: {
        author: String,
        genre: String,
        poster: String,
        title: String,
        year: String,
    }

}
</script>

<style lang="scss" scoped>

@import "../assets/stiles/variables.scss";

        .disk {
            background-color: #2E3A46;
            width: calc((100% / 5) - 2rem);
            text-align: center;

            img {
                width: 100%;
                padding: 2rem;
            }

            h2 {
                padding: 1rem 2rem;
                font-size: 2rem;
            }

            p {
                color: $subTextColor;

            }

            &:last-child {
                padding-bottom: 7rem;
            }
        }



</style>