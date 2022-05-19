export default {
  data: () => ({
    pokemonList: []
  }),
  async mounted() {
    const pokeData = await fetch('https://pokeapi.co/api/v2/region/1/').then(
      Response => Response.json()
    )

    this.pokemonList = pokeData.pokemon_entries
  }
}