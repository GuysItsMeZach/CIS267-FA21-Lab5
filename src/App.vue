<template>
  

  <PartyPokemon 
    :partyPokemon="pp"
    @remove-pokemon="remove"
    />
    <AllPokemon 
    :partyPokemon="allPokemon"
    @remove-pokemon="addPokemonToParty"
    @add-more="addMore"
    />

  <footer> &copy; 2021 </footer>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import PartyPokemon from "./components/PartyPokemon.vue"
import AllPokemon from "./components/AllPokemon.vue"

export default {
  name: 'App',
  components: {
    PartyPokemon,
    AllPokemon
  },
  data() {
    return {
      pp: [],
      allPokemon: [],
      pokemonCount: 151,
      maxPartySize: 6,
    }
  },
  methods: {
    remove(pokemon) {
      this.pp = this.pp.filter( p => p.guid!= pokemon.guid);
    },

    async loadPokemon() {
      // load all pokemon from API and save into all pokemon
      let pokemon = [];
      for (let i = 1; i <= this.pokemonCount; i++) {
        let p = await this.getPokemon(i);
        if (p.name === "mr-mime") {
          p.name = "Mr. Mime";
        }
        p.isFavorite = false;

        pokemon.push(p);
      }

      pokemon.forEach( p => {
          this.allPokemon.push(p);
      });
    },
    async getPokemon(id) {
      // get pokemon data from pokeapi
      const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
    
      const response = await fetch(url);
      const data = await response.json();
    
      return data;
      //createPokemonCard( data );
    },
    addPokemonToParty(pokemon) 
    {
      if (this.pp.length  < 6) {
        const pokemonCopy = {...pokemon};
        pokemonCopy.guid = this.getGUID();
        this.pp.push(pokemonCopy);
      }
    },
    removePokemonFromParty(pokemon) {      
      this.partyPokemon = this.partyPokemon
                            .filter( p => p.guid != pokemon.guid);
    },
    
    getGUID() {
      return Math.floor(Math.random()* 1000000);
    },
    
  },
  mounted() {
    this.loadPokemon();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: linear-gradient(to right, #d4d3dd, #efefbb);
}
</style>
