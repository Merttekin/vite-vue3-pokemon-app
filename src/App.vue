<template>
  <div id="app">
    <h1>Pokémon Explorer</h1>
    <div class="content">
      <PokemonList @selectPokemon="getPokemonDetails" />
      <PokemonDetail v-if="selectedPokemon" :pokemon="selectedPokemon" />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import PokemonList from "./components/PokemonList.vue";
import PokemonDetail from "./components/PokemonDetail.vue";
import axios from "axios";

export default {
  components: {
    PokemonList,
    PokemonDetail,
  },
  setup() {
    const selectedPokemon = ref(null);

    const getPokemonDetails = async (url) => {
      const response = await axios.get(url);
      selectedPokemon.value = response.data;
    };

    return {
      selectedPokemon,
      getPokemonDetails,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin-top: 30px;
}

h1 {
  font-size: 2.5rem;
  color: #2c3e50;
}

.content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-top: 20px;
}

.content > * {
  flex: 1;
  margin: 0 10px;
}
</style>
