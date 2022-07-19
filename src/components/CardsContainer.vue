<template>
    <div class="container" v-if="disks.length === 10">

        <DiskCard v-for="(disk, index) in disks" :key="index"
            
            :author="disk[index].author"
            :genre="disk[index].genre"
            :poster="disk[index].poster"
            :title="disk[index].title"
            :year="disk[index].year"
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
        }
    },

    methods: {
        getDisksList: function() {

            for (let i = 0; i < 10; i++) {

                axios.get("https://flynn.boolean.careers/exercises/api/array/music")
                    .then((response) => {
                        this.disks.push(response.data.response);
                    }
                )
            }

        }

    },

    created() {
        this.getDisksList();
    },

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