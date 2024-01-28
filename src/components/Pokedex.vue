<template>
  <div>
    <input class="pokemon-input" type="number" v-model="pokemonCount" placeholder="Nombre de Pokémon" />

    <select class="pokemon-input" v-model="selectedGen">
      <option v-for="gen in generation" :key="gen" :value="gen">
        Generation {{ gen }}
      </option>
    </select>

    <button class="pokemon-input" @click="loadPokemon">Charger</button>
    <ListeGenerations :pokemon-list="pokemonList" />
    <div class="pokedex">
      <PokemonCard v-for="pokemon in pokemonList" :key="pokemon.id" :pokemon-data="pokemon" />
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import PokemonCard from './Pokemon.vue';
import ListeTypesPokemon from './ListeTypesPokemon.vue';

export default {
  components: {
    PokemonCard,
    ListeTypesPokemon
  },
  data() {
    return {
      pokemonList: [],
      pokemonCount: 20,
      generation: ['1', '2', '3', '4', '5', '6', '7', '8'],
      selectedGen: '1'
    };
  },
  methods: {
    loadPokemon() {
      let apiUrl = `https://pokebuildapi.fr/api/v1/pokemon`;

      if (this.selectedGen) {
        apiUrl += `/generation/${this.selectedGen}`;
      }

      axios.get(apiUrl)
        .then((response) => {
          this.pokemonList = response.data.slice(0, this.pokemonCount);
        })
        .catch((error) => {
          console.log(error);
        });
    }
  },
  mounted() {
    this.loadPokemon();
  },
};
</script>

<style scoped>
.pokedex {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.pokemon-input {
  padding: 10px;
  font-size: 16px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #333;
  color: #FFF;
}
</style>
