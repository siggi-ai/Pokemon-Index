<template>
  <div class="detailContainer">
    <h3>Classification</h3>
    <!-- {{ pokemon }} -->
    <div v-if="apiResponseData.name" class="detailText">
      <p style="color: Plum">id: {{ apiResponseData.id }}</p>
      <br />
      <p style="color: Tomato">name: {{ pokemon.name }}</p>
      <br />
      <p style="color: CornflowerBlue">
        abilities: {{ apiResponseData.abilities[0].ability.name }}
      </p>
      <br />
      <p style="color: limegreen" v-if="apiResponseData.name">
        move: {{ apiResponseData.moves[0].move.name }}
      </p>
      <br />
      <p style="color: gray">height: {{ apiResponseData.height }}</p>
      <br />
      <p style="color: CadetBlue">weight: {{ apiResponseData.weight }}</p>
      <br />
    </div>
    <div v-else class="welcome">
      <h1>Welcome to the Pokédex!</h1>
      <p>⚡</p>
      <h3>please click the detail buttons (left)</h3>
      <p>⚡</p>
      <h4>You will find all the first original 151 Pokémon and more.</h4>
    </div>
    
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      apiResponseData: {},
    };
  },
  props: {
    pokemon: {
      default: {},
    },
  },
  watch: {
    pokemon: async function () {
      try {
        /* console.log(this.pokemon.url); */
        const response = await fetch(this.pokemon.url);
        const result = await response.json();
        this.apiResponseData = result;
        console.log(result);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
.detailContainer {
  background-color: rgb(255, 230, 0);
  border: solid 2px black;
  width: 100%;
}

.welcome {
  font-family: "Press Start 2P", cursive;
  font-size: 1 em;
  text-align: center;
  align-content: center;
  margin-left: 25px;
  margin-right: 30px;
  padding: 10px;
  padding-right: 25px;
  background-color: #ffff94;
  border-radius: 2%;
}

.detailText {
  font-family: "Press Start 2P", cursive;
  width: 70%;
  margin: 50px;
  margin-top: 40px;
  font-size: large;
  font-weight: normal;
  background-color: #ffff94;
  border-radius: 2%;
  padding: 20px;
}

h1 {
  margin-left: 25px;
}

h3 {
  margin-left: 25px;
  margin-top: 37px;
}

h4 {
  margin-left: 25px;
}
</style>