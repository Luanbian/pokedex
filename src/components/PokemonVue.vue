<template>
    <div id="pokemon">
      <div class="card">
        <div class="card-image">
          <figure>
            <img :src="currentImage" alt="Placeholder image"/>
          </figure>
        </div>
        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4">{{upper(name)}}</p>
              <p class="subtitle is-6">{{pokemon.type}}</p>
            </div>
          </div>
          <div class="content">
            <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar Sprite</button>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImage = this.pokemon.front
    });
  },
  data() {
    return {
      isfront: true,
      currentImage: '',
      pokemon: {
        type: '',
        front: '',
        back: ''
      }
    }
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  computed: {
    upper() {
      return (value) => {
        const newName = value[0].toUpperCase() + value.slice(1);
        return newName;
      };
    },
  },
  methods:{
    mudarSprite: function(){
       this.isfront = !this.isfront
       this.isfront ? this.currentImage = this.pokemon.back : this.currentImage = this.pokemon.front
    }
  }
};
</script>

<style>
    #pokemon{
        margin-top: 10%;
    }
</style>
