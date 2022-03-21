<template>
  <div class="pictureContainer">
    <a href="https://portfolio-siggi-ai.herokuapp.com/webPages" class="homeLink">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;back to portfolio</a>
    <div v-if="apiResponseData.name" class="pictureBox">
      <div id="pokeImage"></div>
      <img
        v-if="apiResponseData.name"
        :src="apiResponseData.sprites.other['official-artwork'].front_default"
        width="250"
      />
    </div>
    <div v-else class="welcome">🏯</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      apiResponseData: {},
    };
  },
  props: {
    pokemon: {
      default: {},
    },
    picture: {
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
        console.log(result.sprites.front_default);
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style scoped>
#pokeImage {
  padding-top: 160px;
  padding-left: 20px;
}

.pictureContainer {
  background-color: rgb(115, 238, 110);
  border: solid 2px black;
  width: 100%;
  /* background-image: url("https://cdn130.picsart.com/263776559023212.png"); */
  background-image: url("/images/Radius_18.jpg");
  padding-top: 10px;
  padding-right: 10px;
  background-size: 487px 650px;
  background-repeat: no-repeat;
  background-size: cover;
}

.pictureBox {
  height: 78%;
  width: 100%;
  margin-left: 130px;
  /* margin: 0 auto; */
  /* margin-left: 110px;
  margin-top: 40px; */
  font-size: medium;
  font-weight: bold;
}

.welcome {
  font-family: "Press Start 2P", cursive;
  font-size: 300px;
  align-content: center;
  background-color: rgb(115, 238, 110);
  margin-left: 20px;
  margin-top: 20px;
  padding-top: 27px;
  padding-left: 5px;
  width: 94%;
  height: 529px;
}
</style>
