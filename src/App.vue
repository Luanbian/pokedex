<template>
<div id="app">
  <div class="column is-half is-offset-one-quarter">
    <div v-for="(poke, index) in pokemons" :key="index">
      <PokemonVue :name="poke.name" :url="poke.url" :num="index"/>
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
      pokemons: []
    }
  },
  created : function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=152&offset=0").then(res => {
      this.pokemons = res.data.results
    })
  },
  components:{
    PokemonVue
  }
}
</script>