<template>
  <div class="pokemon-card" @click="goToDetails" :style="{ backgroundColor: getTypeColor() }">
    <p class="pokemon-name">{{ pokemonData.name }}</p>
    <img :src="pokemonData.image" alt="Pokemon Image" class="pokemon-image">
    <div v-for="type in pokemonData.apiTypes" :key="type.name" class="type-info">
      <p>{{ type.name }}</p>
      <img :src="type.image" alt="Type Image" class="type-image">
    </div>
    <p class="generation-info">Génération: {{ pokemonData.apiGeneration }}</p>
  </div>
</template>

<script>
export default {
  props: {
    pokemonData: {
      type: Object,
      required: true,
    },
  },
  methods: {
    goToDetails() {
      this.$router.push({ name: 'DetailsPokemon', params: { id: this.pokemonData.id } });
    },
    getTypeColor() {
      const firstType = this.pokemonData.apiTypes.length > 0 ? this.pokemonData.apiTypes[0].name : null;

      switch (firstType) {
        case 'Plante':
          return 'lightgreen';
        case 'Feu':
          return 'salmon';
        case 'Psy':
          return 'plum';
        case 'Sol':
          return 'burlywood';
        case 'Eau':
          return 'lightblue';
        case 'Poison':
          return 'mediumorchid';
        case 'Combat':
          return 'sienna';
        case 'Vol':
          return 'deepskyblue';
        case 'Insecte':
          return 'palegoldenrod';
        case 'Fée':
          return 'lightpink';
        case 'Roche':
          return 'saddlebrown';
        case 'Électrik':
          return 'gold';
        case 'Spectre':
          return 'darkorchid';
        case 'Acier':
          return 'slategray';
        case 'Glace':
          return 'aquamarine';
        case 'Dragon':
          return 'darkred';
        case 'Ténèbres':
          return 'dimgray';
        default:
          return 'gray';
      }
    }
  }
};
</script>

<style scoped>
.pokemon-card {
  border: 2px solid #333;
  padding: 15px;
  margin: 15px;
  width: 200px;
  text-align: center;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.pokemon-card:hover {
  background-color: #f0f0f0;
}

.pokemon-name {
  font-size: 20px;
  font-weight: bold;
  color: #333;
}

.pokemon-image {
  width: 150px;
  height: 150px;
  margin: 10px 0;
}

.type-info {
  margin-top: 10px;
}

.type-image {
  width: 50px;
  height: 50px;
  margin: 5px;
}

.generation-info {
  margin-top: 10px;
  font-style: italic;
  color: #555;
}
</style>
