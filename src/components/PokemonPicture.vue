<template>
  <div class="pokemon-container">
    <img :src="imgSrc" 
          alt="img del pokemon"
          class="hidden-pokemon">

    <img v-if="showPokemon" :src="imgSrc" 
          alt="img del pokemon"
        class="fade-in">

  </div>

</template>

<script>
export default {

  props: {
    pokemonId:{
      type: Number,
      required: true,
      default :0
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false
    }
  },

  data(){
    return {

    }
  },
  computed: {
    imgSrc () {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokemonId}.svg`
    }
  }

}
</script>

<style scoped>

.pokemon-container {
  height: 200px;
}

img {
  height: 200px;
  position: absolute;
  right: 42%;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-select: none;
  -webkit-user-drag: none;
}

.hidden-pokemon {
  filter: brightness(0);
}

</style>