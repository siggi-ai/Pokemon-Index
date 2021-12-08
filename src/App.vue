<template>
  <div class="mainContainer">
    <link
      href="https://fonts.googleapis.com/css2?family=Dela+Gothic+One&display=swap"
      rel="stylesheet"
    />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap"
      rel="stylesheet"
    />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Knewave&display=swap"
      rel="stylesheet"
    />
    <List @onClick="handleClick" />
    <Detail :pokemon="chosenPokemon" />
    <Picture :pokemon="chosenPokemon" />
  </div>
</template>

<script>
import List from "./components/List.vue";
import Detail from "./components/Detail.vue";
import Picture from "./components/Picture.vue";

export default {
  components: {
    List,
    Detail,
    Picture,
  },
  data: function () {
    return {
      chosenPokemon: {},
    };
  },
  methods: {
    handleClick: function (pokemon) {
      /*       console.log(pokemon); */
      this.chosenPokemon = pokemon;
    },
  },
};

// Homework

// - Style it nicely...
// - as you style, consider creating smaller components if needed
// - represent all the different values from the Pokemon in the Detail
// - only image is mandatory

// - add pagination to the List (prv and nxt buttons)
// - buttons should only be enabled if there is a pre or nxt
// - make sure you understand the whole functionality, take time to understand properly
// - have fun!
</script>

<style scoped>
.mainContainer {
  display: flex;
  flex-direction: row;
  margin: 30px;
  font-family: "Dela Gothic One", cursive;
}
</style>
