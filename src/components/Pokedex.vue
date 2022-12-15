<template>
  <div class="container">
    <PokemonSearch @searchPokemonEmit="barRecherche"/>
    <PokemonDetail @closeDetail="closeDetail" :visible="visible" :pokemonUrl="pokemonUrl" />
    <PokemonList @showPokemonDetailEmit="pokemonetafficher" :recherche="this.recherche" />
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue";
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue";

export default {
  data: function () {
    return{
      visible: false,
      pokemonUrl:"",
      pokemonImage:"",
      recherche : ""   
    }},
  
  

  components: {
    PokemonDetail,
    PokemonList,
    PokemonSearch,
  },

  methods:{
    pokemonetafficher(pokemonUrl){
      this.pokemonUrl = pokemonUrl
      this.visible=true
    },

    pokemonImageData(pokemonImage){
      this.pokemonImage = pokemonImage
    },

    closeDetail(){
      this.visible=false
    },
    barRecherche(recherche) {
      this.recherche = recherche
    },
  }
};

</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>