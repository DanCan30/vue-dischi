<template>
  
    <div class="disk">

        <div class="img-container">
            <img :src="poster" :alt="`${title} performed by ${author}`">
            <span>{{ genre }}</span>
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
            background-color: rgba(255, 255, 255, .1);
            width: calc((100% / 5) - 2rem);
            text-align: center;
            cursor: pointer;
            transition: .3s;

            .img-container {
                position: relative;
                overflow: hidden;
                padding: 2rem;
    
                img {
                    width: 100%;
                    background-color: black;
                }

                span {
                    position: absolute;
                    top: 50%;
                    
                    transform: translate(50%, -50%);
                    font-size: 2rem;
                    font-weight: bolder;
                }
            }

            h2 {
                padding: 1rem 2rem;
                font-size: 2rem;
            }

            p {
                color: $subTextColor;

            &:last-child {
                padding-bottom: 2rem;
            }

            }

            &:hover {
                background-color: rgba(0, 0, 0, .5);

                span {
                    animation: slide .3s forwards;

                    @keyframes slide {
                        0% {
                            right: 0;
                        }

                        100% {
                            right: 50%;
                        }
                    }
                }

                img {
                    opacity: .1;
                }
            }
        }



</style>