<template>
  <div class="listContainer">
    <h1>Pokédex!</h1>

    <div
      class="list"
      v-for="(pokemon, index) in apiResponseData.results"
      :key="index"
    >
      <span>{{ apiResponseData.id }}&nbsp;{{ pokemon.name }}</span>
      <button class="detailButton" @click="handleClick(pokemon)">
        details
      </button>
    </div>

    <br />
    <div class="paginateButtons">
      <div class="prevButton">
        <button value="10" @click="prevMethod" :disabled="isDisabled">
          Prev
        </button>
      </div>
      <div class="nextButton">
        <button @click="nextMethod">GO!</button>
      </div>
      <br />
      <br />
      <div class="counter" v-if="counter > 0">
        &nbsp;{{ counter }}-{{ counter + 10 }}&nbsp;
      </div>
    </div>
    <br />
    <br />
  </div>
</template>

<script>
export default {
  emits: ["onClick", "prevClick", "nextClick"],
  data: function () {
    return {
      apiResponseData: {},
      offset: 0,
      counter: 0,
    };
  },
  mounted: async function () {
    const url = `https://pokeapi.co/api/v2/pokemon/?offset=0&limit=10"`;
    try {
      const response = await fetch(url);
      const result = await response.json();
      this.apiResponseData = result;
      console.log(result);
    } catch (error) {
      console.log(error);
    }
  },
  updated: async function () {
    const offset = this.counter;
    const url = `https://pokeapi.co/api/v2/pokemon/?offset=${offset}&limit=10"`;
    try {
      const response = await fetch(url);
      const result = await response.json();
      this.apiResponseData = result;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    handleClick: function (pokemon) {
      /* console.log(pokemon.url); */
      /* alert(pokemon.name); */
      this.$emit("onClick", pokemon);
    },
    prevMethod: function (counter) {
      this.counter = this.counter - 10;
      console.log(counter);
      this.$emit("prevClick", counter);
    },
    nextMethod: function (counter) {
      this.counter = this.counter + 10;
      console.log(counter);
      this.$emit("nextClick", counter);
    },
  },
  computed: {
    isDisabled() {
      // you can  check your form is filled or not here.
      return this.counter <= 0 == true;
    },
  },
};
</script>

<style scoped>
.listContainer {
  background-color: aliceblue;
  border: solid 2px black;
  width: 100%;
  background-color: red;
}

.list {
  margin: 20px;
  font-size: large;
  font-weight: normal;
  color: white;
}

.detailButton {
  float: right;
  margin-right: 100px;
  margin-top: 10px;
  background: #ff9f9f;
  border-radius: 5px;
  font-family: "Press Start 2P", cursive;
  font-size: 10px;
}

.paginateButtons {
  display: flex;
  margin-left: 170px;
  border: 20px;
  font-family: "Press Start 2P", cursive;
}

.nextButton {
  margin-left: 30px;
  font-family: "Press Start 2P", cursive;
}

.prevButton {
  font-family: "Press Start 2P", cursive;
}

.prevButton:disabled,
Button[disabled]{
  border: 1px solid #999999;
  background-color: #cccccc;
  background-image: url("http://img4.wikia.nocookie.net/__cb20140520015336/pokemon-fano/images/6/6f/Poke_Ball.png");
  color: #666666;
  border-radius: 2%;
}

span {
  margin-left: 50px;
}

h1 {
  margin-left: 25px;
}

.counter {
  padding-top: 3px;
  margin: 0 auto;
  background-color: #9c9c9c;
  display: flex;
  flex-direction: column;
  border-radius: 2%;
}
</style>
