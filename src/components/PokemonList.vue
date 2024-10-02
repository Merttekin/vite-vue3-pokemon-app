<template>
  <div class="pokemon-list">
    <div v-for="(pokemon, index) in pokemonList" :key="index" class="pokemon-item">
      <button @click="$emit('selectPokemon', pokemon.url)">
        {{ pokemon.name }}
      </button>
    </div>
    <div class="pagination">
      <button @click="prevPage" :disabled="!previous">Previous</button>
      <button @click="nextPage" :disabled="!next">Next</button>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  setup() {
    const pokemonList = ref([]);
    const next = ref(null);
    const previous = ref(null);
    const apiUrl = ref("https://pokeapi.co/api/v2/pokemon?limit=10");

    const fetchPokemon = async (url) => {
      const response = await axios.get(url);
      pokemonList.value = response.data.results;
      next.value = response.data.next;
      previous.value = response.data.previous;
    };

    const nextPage = () => {
      if (next.value) {
        fetchPokemon(next.value);
      }
    };

    const prevPage = () => {
      if (previous.value) {
        fetchPokemon(previous.value);
      }
    };

    onMounted(() => {
      fetchPokemon(apiUrl.value);
    });

    return {
      pokemonList,
      nextPage,
      prevPage,
      next,
      previous,
    };
  },
};
</script>

<style scoped>
.pokemon-list {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.pokemon-item {
  margin: 5px 0;
}

button {
  background-color: #3498db;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  width: 100%;
  text-align: left;
}

button:hover {
  background-color: #2980b9;
}

.pagination {
  margin-top: 20px;
}

button:disabled {
  background-color: #95a5a6;
  cursor: not-allowed;
}
</style>
