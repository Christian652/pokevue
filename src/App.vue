<template>
  <div id="app">
    <div class="column">
      <h2>Pesquise</h2>
      <input type="text" class="input is-rounded" v-model="searchValue">
    </div>
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(pokemon, index) in find" :key="pokemon.name">
       <Pokemon :name="pokemon.name" :url="pokemon.url" :num="++index" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      searchValue: ''
    }
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(response => {
      this.pokemons = response.data.results
    })
  },
  components: {
    Pokemon
  },
  computed: {
    find() {
      if (this.searchValue == "" || this.searchValue == " ") {
        return this.pokemons
      } else {
        let pokemons = this.pokemons.filter(pokemon => {
          return pokemon.name == this.searchValue
        })

        if (pokemons.length == 0) {
          return this.pokemons
        } else {
          return pokemons
        }
      }
    }
  }
}
</script>

<style>
  
</style>
