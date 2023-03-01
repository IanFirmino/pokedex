<template>
    <div id="app">
        <div class="column is-half is-offset-one-quarter"> 
          <img src="./assets/logo.png">
          <hr>
          <h4 class="is-size-4">Pokedex</h4>
          <input class="input is-rounded" type="text" v-model="busca" placeholder="Procure um pokemon pelo nome">
          <button class="button is-sucess" id="buscar" @click="buscar">Buscar</button>
          <div v-for="(poke, index) in filteredPokemons" :key="poke">
            <pokemonVue :num="index" :name="poke.name" :url="poke.url" />
          </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import pokemonVue from './components/pokemonVue.vue';

export default {
  name: 'App',
  
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },

  created(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = this.pokemons
    })
  },

  components: {
    pokemonVue
  },

  methods:{
    buscar(){
      if(this.busca != ''){
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }else{
        this.filteredPokemons = this.pokemons;
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

#buscar{
  margin-top: 2%
}
</style>
