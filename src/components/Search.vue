<template>

  <div>
    <label for="genre-filter">Filter by {{ type }} </label>
  
    <select name="genre-filter" id="genre-filter" v-model="selectedElement" >

        <option v-for="(content, index) in contents" :key="index" :value="index">
          {{ content.toUpperCase() }}
        </option>

    </select>

      <a href="#" @click="$emit('search', contents[selectedElement])">Search</a>
  </div>

</template>

<script>
export default {

  props: {
    type: String,
    contents: Array,
  },

  data: function() {
    return {

      selectedElement: "",
    }
  },

}
</script>

<style lang="scss" scoped>

@import "../assets/stiles/variables.scss";

div {

  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-top: 1rem;
  
  label {
    text-transform: uppercase;
    font-size: 1.5rem;
  }
  
  select {
    font-size: 2rem;
    background-color: transparent;
    color: white;
    border: none;
    border-bottom: 2px solid black;
    border-right: 2px solid black;
    outline: none;
    margin-left: 2rem;
  
    option {
      background-color: $bgColor;
      color: white;
    }
  }
      
  a {
    color: $bgColor;
    background-color: #18D860;
    display: inline-block;
    padding: .5rem 1rem;
    font-size: 1.5rem;
    border-radius: 30px;
    text-decoration: none;
    margin: 0 2rem;
  }
}
</style>