<template>
  <div class="pokemon-list">
    <h2>Nombre de Pokémon par type:</h2>
    <ul>
      <li v-for="(count, type) in typeCounts" :key="type">
        {{ type }}: {{ count }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'ListeTypesPokemon',
  props: {
    pokemonList: {
      type: Array,
      required: true
    }
  },
  computed: {
    typeCounts() {
      const counts = {};
      this.pokemonList.forEach(pokemon => {
        pokemon.apiTypes.forEach(typeObj => {
          const type = typeObj.name;
          if (!counts[type]) {
            counts[type] = 0;
          }
          counts[type]++;
        });
      });
      return counts;
    }
  }
};
</script>

<style scoped>
.pokemon-list {
  padding: 0;
}

.pokemon-list li {
  border: 1px solid #ccc;
  margin: 5px 0;
  padding: 10px;
  background-color: #f8f8f8;
  border-radius: 5px;
}
</style>
