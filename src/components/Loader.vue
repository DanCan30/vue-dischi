<template>
  <section>
    <h2>loading...</h2>
    <div class="loading-bar">
        <div class="loading-percentage"></div>
    </div>
  </section>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>

    section {
        width: 100vw;
        height: 100vh;
        position: absolute;
        top: 0;
        left: 0;
        background-color: rgba(0, 0, 0, .7);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        h2 {
            text-transform: uppercase;
            text-align: center;
            margin-bottom: 1rem;
            font-size: 3rem;
        }

        .loading-bar {
            width: 30rem;
            height: 2rem;
            background-color: lightgrey;
            border-radius: 20px;

            
        .loading-percentage {
            width: 0%;
            height: 100%;
            background-color: #18D860;
            border-radius: 20px;
            animation: loading 1s forwards;
        }

            @keyframes loading {
                0% {
                    width: 0%;

                };

                100% {
                    width: 100%;

                };
            };
        }

        
    }

</style>