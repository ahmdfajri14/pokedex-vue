<template>
  <v-container>
    <v-row align="center" justify="left" id="header">
      <v-col sm="3" align-self="center">
        <div id="header__dot"/>
      </v-col>
    </v-row>
     <v-row align="center" justify="center">
     <div v-if="emptyPokemon" id="home__clean">
       <img src="../assets/egg.svg" alt="Egg" />
        <p>There's no Pokémon here</p>
        <v-btn dark rounded @click="openList()">Search</v-btn>
     </div>
     <div id="list" v-if="!emptyPokemon">
    <PokemonSearch 
      :apiUrl="apiUrl" 
      @setPokemonUrl="setPokemonUrl" />
    <PokemonList 
      :imageUrl="imageUrl" 
      :apiUrl="apiUrl"
      @setPokemonUrl="setPokemonUrl" />
    <PokemonDetail 
      v-if="showDetail"
      :pokemonUrl="pokemonUrl"
      :imageUrl="imageUrl"
      @closeDetail="closeDetail" />
     </div>
    </v-row>
  </v-container>
</template>


<script>
  import PokemonSearch from '../components/PokemonSearch.vue';
  import PokemonList from '../components/PokemonList.vue';
  import PokemonDetail from '../components/PokemonDetail.vue';

  export default {
    data: () => {
      return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
        pokemonUrl: '',
        emptyPokemon: true,
        showDetail: false
      }
    },
    components: {
      PokemonSearch,
      PokemonList,
      PokemonDetail
    },
    methods: {
      openList() {
        this.emptyPokemon = false;
      },
      setPokemonUrl(url) {
        this.pokemonUrl = url;
        this.showDetail = true;
      },
      closeDetail() {
        this.pokemonUrl = '';
        this.showDetail = false;
      }
    }
  }
</script>


<style>
#header {
  position: relative;
  background-color: #E30000;
  color: #fff;
  border-bottom: 5px solid #88001c;
  box-shadow: 0 2px 0 #3B000C; }
  #header:before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background-color: #3B000C; }
#header__dot {
  position: relative;
  width: 45px;
  height: 45px;
  border-radius: 40px;
  background-color: #4D8DFF;
  border: 5px solid #fff;
  margin-right: 30px;
  transition: background-color 50ms ease;
  animation: header-dot-animation 500ms ease infinite alternate; }
  #header__dot:before {
    content: '';
    position: absolute;
    top: 5px;
    left: 5px;
    width: 10px;
    height: 10px;
    border-radius: 10px;
    background-color: rgba(255, 255, 255, 0.75); }
    @keyframes header-dot-animation {
  from {
    background-color: #4D8DFF; }
  to {
    background-color: #9abeff; } }
    
  #home__clean {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding-top: 20px; }
  .home__clean > img {
    width: 100px;
    height: auto; }
  .home__clean > p {
    color: #36383D;
    text-transform: uppercase;
    font-weight: bold; }

    #navigation {
  position: relative;
  background-color: #E30000;
  color: #fff;
  border-top: 1px solid #88001c;
  box-shadow: 0 -2px 0 #3B000C; }
   #navigation:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background-color: #3B000C; }

 #navigation__container {
  display: flex;
  align-items: center;
  min-height: 56px; }

 #navigation__list {
  display: flex;
  width: 100%;
  justify-content: space-between;
  padding: 0;
  margin: 10px 0;
  list-style: none; }

 #navigation__item {
  flex: 1; }
   #navigation__item:first-child >  #navigation__link {
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px; }
   #navigation__item:last-child >  #navigation__link {
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    border-right: none; }

#navigation__link {
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  min-height: 80px;
  max-height: 80px;
  min-width: 120px;
  text-transform: uppercase;
  text-decoration: none;
  font-size: 14px;
  color: #fff;
  background-color: #4D8DFF;
  border-right: 1px solid #001c4d;
  border-bottom: 3px solid #001c4d; }
  #navigation__link:hover {
    background-color: #015cff; }

#navigation__icon {
  height: 30px;
  width: auto; }

#list{
   display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 10px;
    width: calc(100% - 20px);
    min-height: calc(100vh - 20px);
    font-family: 'Acme', arial;
    font-size: 1rem;
    font-weight: normal;
}
</style>
