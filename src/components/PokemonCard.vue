<template>
  <!-- <div class="pokemon" @click="click">
    <h1>{{ pokemon.name }}</h1>

    <h2>{{ pokemon.id }}</h2>
  </div> -->
  <!-- :style="{background: backgroundColor(pokemon)} -->
  <div class="pokemon" @click="click" :style="{background: backgroundColor}">
    <div class="img-container">
      <img
          :src="pokemon.sprites.other['official-artwork'].front_default"
        />
    </div>
    <div class="info">
      <span class="number">#{{pokemon.id}}</span>
      <h3 class="name">{{pokemon.name}}</h3>
      <small class="type">
        {{typeText}}
      </small>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonCard",
  props: {
    pokemon: Object,
    clickAction: String,
    test: String,
  },
  data() {
    return {
      colors: {
        fire: '#fd7d24',
        grass: '#9bcc50',
        electric: '#eed535',
        water: '#4592c4',
        ground: '#ab9842',
        rock: '#a38c21',
        fairy: '#fdb9e9',
        poison: '#b97fc9',
        bug: '#729f3f',
        dragon: '#7038f8',
        psychic: '#f366b9',
        flying: '#3dc7ef',
        fighting: '#d56723',
        normal: '#a4acaf',
        ice: '#51c4e7',
        ghost: '#7b62a3',
        dark: '#707070',
        steel: '#9eb7b8'
      }
    };
  },
  methods: {
    click() {
      this.$emit("click-pokemon", this.pokemon);
    },
  },
  computed: {
    typeText() {
      const type1 = this.pokemon.types[0].type.name;
      const type2 = this.pokemon.types.length > 1 ? this.pokemon.types[1].type.name : null;
      if (type2 != null) {
        return `${type1} / ${type2}`;
      }
      else {
        return `${type1}`;
      }

    },
    backgroundColor() {
      const type1 = this.pokemon.types[0].type.name;
      const type2 = this.pokemon.types.length > 1 ? this.pokemon.types[1].type.name : null;
      const color = this.colors[type1];
      if (type2 != null) {
          const color2 = this.colors[type2];
          return `linear-gradient(to right, ${color} , ${color2})`;
      }
      else {
          return color;
      }
    }
  }
};
</script>

<style>
.pokemon {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex-basis: 15%;
  background-color: #eee;
  border-radius: 10px;
  box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
  margin: 10px;
  padding: 20px;
  text-align: center;
  transform: scale(1);
  transition: all 0.2s;
  cursor: pointer;
}

.pokemon:hover {
  transform: scale(1.05);
}

.pokemon .img-container {
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  width: 100px;
  height: 100px;
  text-align: center;
}

.pokemon .img-container img {
  /* max-width: 90%; */
  width: 120%;
  margin-top: 00px;
}

.pokemon .info {
  margin-top: 20px;
}

.pokemon .info .number {
  background-color: rgba(0, 0, 0, 0.1);
  padding: 5px 10px;
  border-radius: 10px;
  font-size: 0.8em;
}

.pokemon .info .name {
  font-family: "Playfair Display", serif;
  font-weight: 400;
  margin: 15px 0 7px;
  letter-spacing: 1px;
}

.pokemon .info small {
  font-size: 0.7em;
  text-transform: capitalize;
  font-weight: 200;
}
</style>
