<template>
  <div class="container">
    <h2>Pockedex</h2>
    <div class="box is-flex is-flex-wrap-wrap is-align-content-center">
      <input type="text" placeholder="Buscar pokemon pelo nome" class="input is-rounded m-5" v-model="buscar">
      <button class="button is-fullwidth is-success" @click="buscarPokemon" >Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :num="index + 1" :name="poke.name" :url="poke.url" />
      </div>
    </div>
    
    </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';
export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      buscar: '',
      filteredPokemons: [],
    }
  },
  created() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(res => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      })
  },
  components: {
    Pokemon
  },
  methods: {
    buscarPokemon() {
      this.filteredPokemons = this.pokemons
      if(this.buscar == '' || this.buscar == " ") {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.buscar.toLowerCase())
      }
    }
  }
}


</script>