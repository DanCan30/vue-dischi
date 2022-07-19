<template>
    <div class="container" v-if="loaded === true">

        <DiskCard v-for="(disk, index) in disks" :key="index"
            
            :author="disk.author"
            :genre="disk.genre"
            :poster="disk.poster"
            :title="disk.title"
            :year="disk.year"
        />



    </div>

    <Loader v-else />

</template>

<script>

import axios from "axios";
import DiskCard from "./DiskCard.vue";
import Loader from "./Loader.vue";

export default {

    components: {
        DiskCard,
        Loader,
    },

    data: function() {
        return {
            disks: [],

            loaded: false,
        }
    },

    methods: {
        getDisksList: function() {

            axios.get("https://flynn.boolean.careers/exercises/api/array/music")
                .then((response) => {
                    this.disks = response.data.response;
                    console.log(this.disks);
                }
            )
        },

        loadingScreen: function() {
            setTimeout( () => {this.loaded = true} , 1500);

        }

    },

    created() {
        this.getDisksList();
    },

    mounted() {
        this.loadingScreen();
    }

}
</script>

<style lang="scss" scoped>

@import "../assets/stiles/variables.scss";

    div.container {
        width: 60%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;

    }

</style>