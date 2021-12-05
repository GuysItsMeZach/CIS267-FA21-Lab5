<template>
  <div id="party">
    <div class="partytext">
      <h2>Party <span class="smallText">{{ partyPokemon.length }}</span>  of <span>6 </span></h2>
    </div>  
    <div class="pokemon-outer" id="party-pokemon" :key="partyKey">
      <PokemonCard 
        class="width"
        v-for="p in partyPokemon" 
        :key="p.id" 
        :pokemon="p" 
        @click-pokemon="remove"
        />
    </div>
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
      
    }
  },
  methods: {
    remove(pokemon) {
      this.$emit("remove-pokemon", pokemon);
    },
    
  }
};
</script>

<style>

.width {
  max-width: 11%;
}
.partytext{
  padding-top: 10px;
  margin-bottom: -40px;
}
.partytext span {
  color:maroon;
}



  </style>
