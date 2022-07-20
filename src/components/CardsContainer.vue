<template>
    <div>
        <Search @search="getDisksList"/>
        <div class="container" v-if="isLoaded === true">


            <DiskCard v-for="(disk, index) in disks" :key="index" 
                
                :author="disk.author"
                :genre="disk.genre"
                :poster="disk.poster"
                :title="disk.title"
                :year="disk.year"
            />



        </div>

        <Loader v-else />
    </div>
</template>

<script>

import axios from "axios";
import DiskCard from "./DiskCard.vue";
import Loader from "./Loader.vue";
import Search from "./Search.vue";

export default {

    components: {
        DiskCard,
        Loader,
        Search,
    },

    data: function() {
        return {
            disks: [],

            isLoaded: false,
        }
    },

    methods: {
        getDisksList: function(genreToFilter) {

            axios.get("https://flynn.boolean.careers/exercises/api/array/music")
                .then((response) => {
                    
                    this.disks = response.data.response;

                    if (genreToFilter == "all") {
                        this.disks = response.data.response;

                    } else {

                        const filteredByGenre = this.disks.filter((disk) => disk.genre.toLowerCase() == genreToFilter.toLowerCase() );
    
                        this.disks = filteredByGenre;
                    }

                }
            )
        },

        loadingScreen: function() {
            setTimeout( () => {this.isLoaded = true} , 1500);

        },

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

    div.container {
        width: 60%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;

    }

</style>