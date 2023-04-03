<template>
  <h1 v-if="!pokemon" >Cargando...</h1>
  <div v-else>
    <h3>Quién es este pokemon?</h3>
    <!-- //TODO IMG -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"/>
    <!-- TODO OPCIONES -->
    <PokemonOptions 
        :pokemons="pokemonArr"
        @selection="checkAnswer"/>

  <template v-if="showAnswer">
    <h2 class="fade-in">{{ message }}</h2>
    <button
      @click="newGame" >
      Nuevo juego
    </button>

  </template>

  </div>
</template>

<script>

import PokemonPicture from './../components/PokemonPicture.vue'
import PokemonOptions from './../components/PokemonOptions.vue'

import getPokemonOptions from '@/helpers/getPokemonOptions'


export default {

  components: {
    PokemonPicture,
    PokemonOptions,
  },
  data () {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: ''
    }
  },
  methods: {
    async mixPokemonArray () {
      this.pokemonArr = await getPokemonOptions()

      const rndInt = Math.floor( Math.random() * 4)
      this.pokemon = this.pokemonArr[rndInt]

    },
    checkAnswer(pokemonId){
      this.showPokemon = true
      this.showAnswer = true

      if (pokemonId === this.pokemon.id) {
        this.message = `Correcto, ${this.pokemon.name}`
      } else {
        this.message = `Oops, era  ${this.pokemon.name}`
      }
    },
    newGame () {
      this.pokemonArr = [],
      this.showPokemon = false,
      this.showAnswer = false,
      this.message = ''
      this.pokemon = null
      this.mixPokemonArray()
    }
  },
  mounted() {
    this.mixPokemonArray()
  }

}
</script>

<style>

</style>
