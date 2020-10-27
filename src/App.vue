<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4>POKEDEX</h4>

      <input class="input is-primary" type="text" name="" id="" v-model="busca">
      <button class="button is-primary" > Buscar </button>

      <!-- <div v-for="(poke, index) in pokemons" :key="index"> -->
      <div v-for="(poke, index) in resultadoBusca" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  data() {
    return {
      pokemons: [],
      busca: ''
    };
  },
  name: "App",
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("pegando os pokemons e salvandos no array");
        this.pokemons = res.data.results;
      });
  },
  components: { 
    Pokemon 
    },
  computed: {
    resultadoBusca: function(){
      if (this.busca == '' || this.busca == ''){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
