<template>
  <div>
    <div v-if="pokemon">
      <h2>{{ pokemon.name }} (Génération: {{ pokemon.apiGeneration }})</h2>
      <div class="center-container">
        <img :src="pokemon.image" alt="Image de Pokémon" class="center-image">
      </div>
      <p>HP: {{ pokemon.stats.HP }}</p>
      <p>Attack: {{ pokemon.stats.attack }}</p>
      <p>Defense: {{ pokemon.stats.defense }}</p>
      <p>Special Attack: {{ pokemon.stats.special_attack }}</p>
      <p>Special Defense: {{ pokemon.stats.special_defense }}</p>
      <p>Speed: {{ pokemon.stats.speed }}</p>
    </div>

    <button class="reload" @click="reloadPokemonDetails">Recharger les détails du Pokémon</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      pokemon: null
    };
  },
  props: {
    id: {
      type: String,
      required: true
    }
  },
  mounted() {
    this.getPokemonDetails();
  },
  methods: {
    getPokemonDetails() {
      axios.get(`https://pokebuildapi.fr/api/v1/pokemon/${this.id}`)
        .then(response => {
          this.pokemon = response.data;
        })
        .catch(error => console.error(error));
    },
    reloadPokemonDetails() {
      this.pokemon = null;
      this.getPokemonDetails();
    }
  }
};
</script>

<style>
body {
  color: #FFF;
}

.center-container {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 300px;
}

.center-image {
  max-width: 100%;
  max-height: 100%;
}

.reload {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #333;
  color: #FFF;
}
</style>
