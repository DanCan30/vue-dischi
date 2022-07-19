<template>
  <div class="container">

    <DiskCard v-for="(disk, index) in disks" :key="index"
        :v-if="disks.length === 9"
        :author="disk.author"
        :genre="disk.genre"
        :poster="disk.poster"
        :title="disk.title"
        :year="disk.year"
    />


  </div>
</template>

<script>

import axios from "axios";
import DiskCard from "./DiskCard.vue";

export default {

    components: {
        DiskCard,
    },

    data: function() {
        return {
            disks: [],
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