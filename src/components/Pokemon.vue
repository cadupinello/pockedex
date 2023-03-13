<template>
  <div>
    <div class="card m-3">
      <div class="card-image">
          <img class="ml-5" :src="this.currentImg" :alt="pokemon.name">
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{name}}</p>
            <p class="subtitle is-6">{{pokemon.type}}</p>
          </div>
        </div>

        <div class="content">
          <button @click="mudarSprite" class="button is-normal">Mudar sprite</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  created() {
    axios.get(this.url)
      .then(res => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.currentImg = this.pokemon.front;
      })
  },
  data() {
    return {
      isFront: true,
      currentImg: '',
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
    url: String
  },
  filters: {
    capitalize: function(value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  },
  methods: {
    mudarSprite() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  }
}
</script>

<style>
  #namePokemon {
    text-transform: capitalize;
  }
  figure {
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  img {
    width: 75%;
  }

</style>