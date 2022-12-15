<template>
  <div class="list">
    <article v-for="(pokemon, index) in filterePokemon" v-bind:key="index" v-on:click="showPokemonDetailEmit(pokemon.url)">
      <h3>{{pokemon.name}}</h3>
      <img :src="image+pokemon.name+'.png'"/>
    </article>
  </div>
</template>

<script>
import conf from '../config/config.json'
import axios from '../../node_modules/axios'
export default {
  props :["recherche"],
  data: function () {
    return{
      pokemons: [],
      image: conf.IMG_URL,
      pokemonUrl: conf.API_URL,
    }
  },
  beforeMount(){
    axios.get(conf.API_URL+'/pokemon') 
    .then((pokemons)=> {
      this.pokemons = pokemons.data.results
    })

  },

  methods: {
    showPokemonDetailEmit(url){
      this.$emit('showPokemonDetailEmit',url)
    },

  },
  computed: {
    filterePokemon: function () {
      return this.pokemons.filter((pokemon) => {
        return pokemon.name.match(this.recherche)
      })
    }
  },
  
};


</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

