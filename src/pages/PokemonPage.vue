<template>
  <h1>¿Quién es este Pokemon?</h1>

  <PokemonPicture :pokemonId="15" :showPokemon="true" />

  <PokemonOptions />
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions";
export default {
  components: {
    PokemonPicture,
    PokemonOptions,
  },
};
</script>

