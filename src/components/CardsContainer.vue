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


                    for (let i = 0; i < this.disks.length; i++) {
                        this.genres.push(response.data.response[i].genre);
                        this.authors.push(response.data.response[i].author);

                    }

                    // Add a new element at the start of the array
                    this.genres.unshift("all");
                    this.authors.unshift("all");

                    // Remove duplicates from array
                    this.genres = [... new Set(this.genres)];
                    this.authors = [... new Set(this.authors)];

                        this.diskInfos = [{type: "genres", content: this.genres,}, {type: "authors", content: this.authors}];

                    if (elementToFilter == "all" || elementToFilter == "") {
                        this.disks = response.data.response;

                    } else {

                        const filteredElement = this.disks.filter((disk) => disk.genre.toLowerCase() == elementToFilter.toLowerCase() || disk.author.toLowerCase() == elementToFilter.toLowerCase() );
                        this.disks = filteredElement;

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