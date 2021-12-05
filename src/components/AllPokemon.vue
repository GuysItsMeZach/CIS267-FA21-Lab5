<template>
  <div id="allPokemon">
    <div class="input-group mb-3">
        <input type="text" class="searchbar" id="searchInput" placeholder="search pokemon name or #" v-model="searchString">
    </div>
    <div class="pokemon-outer" id="party-pokemon" >
      <PokemonCard 
        v-for="p in filteredPokemon" 
        :key="p.id" 
        :pokemon="p" 
        @click-pokemon="remove"
        />
    </div>
    <!-- <h1 v-if="loadingShowing">Loading...</h1> -->
  </div>
</template>

<script>
import PokemonCard from "./PokemonCard.vue"

export default {
  name: "PartyPokemon",
  components: {
    PokemonCard
    },
  props: {
    partyPokemon: Array,
  },
  data() {
    return {
      loadingShowing: false,
      searchString: "",
    }
  },
  methods: {
    remove(pokemon) {
      this.$emit("remove-pokemon", pokemon);
    },
    addMore() {
        this.loadingShowing = true;
        this.$emit("add-more");
    }
  },
  computed: {
      filteredPokemon() {
      let filtered = this.partyPokemon.filter(pokemon => {
        let type2 = pokemon.types.length > 1 ? pokemon.types[1].type.name : null;
        if (pokemon.name.includes(this.searchString.toLowerCase()) || pokemon.id.toString().padStart(3, '0').includes(this.searchString) || pokemon.types[0].type.name.includes(this.searchString)) {
            return true;
        }
        if (type2 != null) {
          if (pokemon.types[1].type.name.includes(this.searchString)) {
              return true;
          }
        }
    });
      return filtered

    },
  }
};
</script>

<style>
.pokemon-outer {
  display: flex;
  flex-direction: row;
  align-items: center;
  flex-basis: 15%;
  border-radius: 10px;
  margin: 10px;
  padding: 20px;
  text-align: center;
  transform: scale(1);
  transition: all 0.2s;
  cursor: pointer;
  overflow: scroll;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin-left: 5vh;
}
#all-pokemon {
  overflow: scroll;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.searchbar {
    width: 25vh;
    height: 25px;
    
}
  </style>
