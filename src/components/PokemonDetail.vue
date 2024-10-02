<template>
  <div class="pokemon-detail">
    <div v-if="pokemon">
      <h2>{{ pokemon.name }}</h2>
      <img :src="pokemon.sprites.front_default" alt="Pokemon Image" />
      <div>
        <h3>Abilities</h3>
        <ul>
          <li v-for="(ability, index) in pokemon.abilities" :key="index">
            {{ ability.ability.name }}
          </li>
        </ul>
      </div>
      <div>
        <h3>Stats</h3>
        <ul>
          <li v-for="(stat, index) in pokemon.stats" :key="index">
            {{ stat.stat.name }}: {{ stat.base_stat }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true,
    },
  },
  filters: {
    capitalize(value) {
      if (!value) return "";
      value = value.toString();
      return value.charAt(0).toUpperCase() + value.slice(1);
    },
  },
};
</script>

<style scoped>
.pokemon-detail {
  margin-top: 20px;
}

h2 {
  font-size: 2rem;
  color: #2c3e50;
}

img {
  max-width: 150px;
  margin: 10px;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
