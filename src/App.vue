<template>
  <div id="app">
    <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="">
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded" type="text" name="filter" placeholder="busque pelo seu pokémon preferido ..." v-model="filter">
      <div v-for="(pokemon, index) in resultFilter" :key="pokemon.name">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :number="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Pokemon from './components/Pokemon';

  export default {
    name: 'App',
    data() {
      return {
        pokemons: [],
        filter: ''
      }
    },
    created: function() { // created é o método chamado assim que o componente for 'criado/chamado' dentro da aplicação(assim como no react temos o componentDidMount)
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
        .then((response) => {
          console.log("Requisição de pokemons feita com sucesso!!!");
          this.pokemons = response.data.results;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally(console.log('Finalizou'));
    },
    components: {
      Pokemon
    },
    computed: {
      resultFilter: function() {
        if(this.filter == '' || this.filter == ' ') {
          return this.pokemons;
        } else {
          return this.pokemons.filter(pokemon => pokemon.name.includes(this.filter));
        }
      }
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
    margin-top: 60px;
  }

  .input {
    margin: 10px 0 25px;
  }
</style>