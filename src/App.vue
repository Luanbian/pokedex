<template>
<div id="app">
  <div class="column is-half is-offset-one-quarter">
    <input 
      type="text" 
      placeholder="Buscar pokemon" 
      v-model="busca"
      class="input is-rounded"
    />
    <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
    <div v-for="poke in filteredPokemons" :key="poke.url">
      <PokemonVue :name="poke.name" :url="poke.url"/>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import PokemonVue from './components/PokemonVue'

export default {
  name: 'App',
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created : function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  components:{
    PokemonVue
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons
      if(this.busca == ''){
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
}
</script>

<style>
  #buscaBtn{
    margin-top: 2%;
  }
</style>