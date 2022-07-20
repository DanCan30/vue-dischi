<template>
    <div>
        <Search @search="getDisksList" 
        v-for="(info, index) in diskInfos" :key="index"
        :type="info.type"
        :contents="info.content" />

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

            genres: [],

            uniqueGenres: [],

            authors: [],

            diskInfos: [],

            isLoaded: false,
        }
    },

    methods: {
        getDisksList: function(elementToFilter) {

            axios.get("https://flynn.boolean.careers/exercises/api/array/music")
                .then((response) => {
                    
                    this.disks = response.data.response;

                    if (elementToFilter == "all") {
                        this.disks = response.data.response;

                    } else {

                        const filteredElement = this.disks.filter((disk) => disk.genre.toLowerCase() == elementToFilter.toLowerCase() || disk.author.toLowerCase() == elementToFilter.toLowerCase() );
                        this.disks = filteredElement;

                    }

                }
            )
        },

        getDiskInfos: function() { 
            axios.get("https://flynn.boolean.careers/exercises/api/array/music")
                .then((response) => {

                    for (let i = 0; i < this.disks.length; i++) {
                        this.genres.push(response.data.response[i].genre);
                        this.authors.push(response.data.response[i].author);

                    }
                    // Remove duplicates from array
                    this.uniqueGenres = [... new Set(this.genres)];


                    // Add a new element at the start of the array
                    this.uniqueGenres.unshift("all");
                    this.authors.unshift("all");

                    this.diskInfos.push({type: "genres", content: this.uniqueGenres,}, {type: "authors", content: this.authors});

                    console.log(this.diskInfos);
                }
            )    



        },

        loadingScreen: function() {
            setTimeout( () => {this.isLoaded = true} , 1500);

        },

    },

    created() {
        this.getDisksList();
        this.getDiskInfos();
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