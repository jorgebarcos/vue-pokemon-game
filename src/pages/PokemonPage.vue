<template>
  <h1 v-if="!pokemon">Espere por favor...</h1>
  <div v-else>
    <h1>¿Quién es este Pokemon?</h1>

    <PokemonPicture :pokemon-id="pokemon.id" :show-pokemon="showPokemon" />

    <PokemonOptions
      :pokemons="pokemonArr"
      @selection-pokemon="checkAnswer($event)"
    />

    <template v-if="showAnswer">
      <h2 class="fade-in">{{ message }}</h2>
      <button @click="newGame">Nuevo Juego</button>
    </template>
  </div>
</template>

<script>
import PokemonPicture from "@/components/PokemonPicture.vue";
import PokemonOptions from "@/components/PokemonOptions";
import getPokemonOptions from "@/helpers/getPokemonOptions";

export default {
  components: {
    PokemonPicture,
    PokemonOptions,
  },
  data() {
    return {
      pokemonArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: "",
    };
  },
  methods: {
    async mixPokemonArr() {
      this.pokemonArr = await getPokemonOptions();

      const rndInt = Math.floor(Math.random() * 4);

      this.pokemon = this.pokemonArr[rndInt];
    },
    checkAnswer(selectedId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (selectedId === this.pokemon) {
        this.message = `Correcto, ${this.pokemon.name} `;
      } else {
        this.message = `Ooops, era ${this.pokemon.name} `;
      }
    },
    newGame() {
      this.pokemonArr = [];
      this.showAnswer = false;
      this.showPokemon = false;
      this.pokemon = null;
      this.mixPokemonArr();
    },
  },
  mounted() {
    this.mixPokemonArr();
  },
};
</script>

