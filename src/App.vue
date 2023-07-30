<template>
  <div id="app">
    <img src="./assets/pokedex.webp" id="logo"><br>
    
    <div class="column is-half is-offset-one-quarter">
      <input type="text" placeholder="Buscar pokémon" v-model="find" class="input is-rounded">
      <button class="button is-fullwidth button is-link" id="find-btn" @click="findP">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
       <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"  /> 
    </div>
    </div>

  </div>
</template>

<script>
import axios from "axios"
import Pokemon from "./components/Pokemon"

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      find: '',
      filteredPokemons: []
    }
  },
 created:function(){
  axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
    this.pokemons = res.data.results
    this.filteredPokemons = res.data.results
  })
 },
 components: {
  Pokemon
 },
 methods: {
  findP: function(){
    this.filteredPokemons = this.pokemons
    if(this.find == ''){
      this.filteredPokemons == this.pokemons
    }else{
      this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.find)
    }
  }
 }
}
</script>

<style>
  #logo{
    max-width: 200px;
    max-height: 200px;
    margin-left: 40%;
    width: auto;
    height: auto;
  }

  #find-btn{
    margin-top: 2%;
  }
</style>
