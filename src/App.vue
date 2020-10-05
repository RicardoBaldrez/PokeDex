<template>
  <div id="app">

  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'App',
    data() {
      return {
        pokemons: []
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
</style>