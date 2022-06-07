<template>
  <h1>Hello_World_2.0</h1>
  <input type='text' v-model='filtertext' />
  <ul>
    <PokedexCard v-for="(pokemon, index) in pokemonStore.filteredList" 
      :key="`poke-${index}`"
      :name="pokemon.pokemon_species.name"
      :number="pokemon.entry_number" />
  </ul>
</template>

<script setup>
import {reactive ,ref, computed, onMounted } from 'vue';
import PokedexCard from './components/PokedexCard.vue'


const pokemonStore = reactive({
   list: [],
   filteredList: computed(() =>
      pokemonStore.list.filter(pokemon =>
        pokemon.pokemon_species.name.includes(filtertext.value)
      )
    ),
})

const filtertext = ref('')

onMounted(async () => {
  const pokeData = await fetch('https://pokeapi.co/api/v2/pokedex/2/').then(
    Response => Response.json()
  )

  pokemonStore.list = pokeData.pokemon_entries
})

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}
</style>

