<template>
  <nav>NAVIGATION</nav>

  <PartyPokemon :partyPokemon="pp" @remove-pokemon="remove" />

  <footer>&copy; 2021</footer>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import PartyPokemon from "./components/PartyPokemon.vue";

export default {
  name: "App",
  components: {
    PartyPokemon,
  },
  mounted() {
    this.loadAllPokemon();
  },

  data() {
    return {
      pp: [
        // {name:"Charmander", id: 3},
        // {name:"Bulbasaur", id: 2},
        // {name:"Pikachu", id: 4}
      ],
    };
  },
  methods: {
    remove(id) {
      this.pp = this.pp.filter((p) => p.id != id);
    },

    async loadAllPokemon() {
      //load all pokemon from API
      //load all pokemon from api and save into allPokemon
      const getPokemon = async function (id) {
        const url = `https://pokeapi.co/api/v2/pokemon/${id}`;

        const response = await fetch(url);
        const data = await response.json();

        return data;
      };
      const pokemon_count = 151;
      let pokemon = [];
      for (let i = 1; i <= pokemon_count; i++) {
        let p = await getPokemon(i);
        if (p.name === "mr-mime") {
          p.name = "Mr. Mime";
        }
      }
      pokemon.forEach((p) => {
        this.allPokemon.push(p);
      });
    },
  },
  
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>