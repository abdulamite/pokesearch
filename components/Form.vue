<template>
    <div>
        <Header />
        <div class="split-container">
            <div class="form-container">
                <div v-if="state == 'loading'" class="loading">
                    <img src="http://chittagongit.com/download/49938">
                </div>
                <h1 v-else>Search for a Pokémon!</h1>
                <el-input id="search" placeholder="Pokemon Name" v-model="search" @keyup.enter.native="fetchData" v-on:keydown.native="showSuggestions" clearable></el-input>
                <el-button @click="fetchData">Get Pokémon</el-button>
                <transition name="fade">
                        <Error v-if="error != ''"/>
                </transition>
                <div id="search_results" v-if="searchResults.length != 809 && searchResults.length > 0">
                    <div v-for="pokemon in searchResults" @click="displayPokemon" class="result">
                            <div class="thumb-image">
                                <img v-bind:src="'https://img.pokemondb.net/artwork/' + pokemon.toLowerCase() + '.jpg'">
                            </div>
                            <p> {{ pokemon }} </p>
                    </div>
                </div>    
            </div>

            <PokemonCard v-bind:pokemon="pokemon" id="pokemon-container"/>
        </div>
    </div>
</template>

<script>
import PokemonCard from '~/components/PokemonCard.vue'
import Error from '~/components/Errors.vue'

const Pokedex = require('pokeapi-js-wrapper');
const P = new Pokedex.Pokedex();
const Vibrant = require('node-vibrant')

// Pull list of pokemon and assign to staticList to cut down network requests
let staticList = async function getPokemon(){
    const pokemon = fetch('https://raw.githubusercontent.com/sindresorhus/pokemon/8310cd9c1342ece30985fb5883e1090e3c56f4a8/data/en.json')
    .then(function(response) {
        return response.json();
    });
    return pokemon;
}


export default {
    components:{
        PokemonCard,
        Error
    },
    name: "Form",
    data(){
        return{
            search: '',
            pokemon: {},
            error: '',
            state: '',
            searchResults: []
        }
    },
    computed:{
        getSprite:function () {
            return `https://img.pokemondb.net/artwork/${this.pokemon}.jpg`
        },
    },
    methods:{
        fetchData:async function(){
            this.state = 'loading';
            try{
                const pokemon = await P.getPokemonByName(this.search.toLowerCase().replace(/(^\s+|\s+$)/g,''))
                .then(function(response) {
                return response;
                });

                console.log(pokemon)
                this.error = '';
                this.pokemon = pokemon;
                this.state = '';

                
            }catch(e){
                this.error = e;
                this.state = '';
            }
        },
        displayPokemon:async function(){
            let clicked;
            if(event.target.nodeName === 'IMG'){
                clicked = event.target.src.split('.')[2].split('/')[2];
            }else{
                clicked = event.target.innerText.toLowerCase();
            }
            this.state = 'loading';
            try{
                const pokemon = await P.getPokemonByName(clicked)
                .then(function(response) {
                return response;
                });

                this.error = '';
                this.pokemon = pokemon;
                this.state = '';
                this.search = clicked;
                this.searchResults = [];

                
            }catch(e){
                this.error = e;
                this.state = '';
            }

        },
        showSuggestions:async function(){
            const pokemonList = await staticList().then(b=>{return (b)});
            let regex = new RegExp("^" + this.search.toLowerCase() + ".*$")
            let searchResults = []
            pokemonList.forEach(pokemon => {
                if (pokemon.toLowerCase().match(regex))
                { 
                    searchResults.push(pokemon)
                }
            });

            this.searchResults = searchResults;
            console.log(this.searchResults.length);
        }
    }

}
</script>

<style scoped>
.split-container{
    display: grid;
    width: 100%;
    height: 100%;
    grid-template-columns: 1fr 3fr;
}

.split-container>*{
    width:50vw;
    height: 100vh;

}


#pokemon-container{
    border-radius: .4rem;
    margin-left: 8em;
    width:75%
}
.form-container{
    text-align:left;
}

.loading {
    width: 100%;
    padding: 0;
    text-align: center;
}

.loading>img{
    height: 100px;
    width: auto;
}

.form-container>*{
    margin:1rem;
}

.el-input{
    width: 75%;
}

#search_results{
    overflow:auto;
    background-color:#e4eae5;
    padding:1rem;
    height:50%;
    border-radius:.3rem;
    max-width: 45%;
    margin:auto;
}

.result{
    padding:1rem;
    padding-top:2rem;
    padding-bottom:2rem;
    background-color:#f8ffff;
    margin:1rem;
    border-radius:.3rem;
    font-weight:bolder;
    display:flex;
    align-items: center;
    justify-content: center;
}
.result>p{
    margin-left:1rem;
}

.result>.thumb-image>img{
    width: 100px;
}


.fade-enter-active, .fade-leave-active {
  transition: opacity .3s ease-in-out;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

</style>