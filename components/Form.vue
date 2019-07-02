<template>
    <div>
        <Header />
        <div class="split-container">
            <div class="form-container">
                <div v-if="state == 'loading'" class="loading">
                    <img src="http://chittagongit.com/download/49938">
                </div>
                <h1 v-else>Search for a Pokémon!</h1>
                <el-input id="search" placeholder="Pokemon Name" v-model="search" @keyup.enter.native="fetchData" clearable></el-input>
                <el-button @click="fetchData">Get Pokémon</el-button>
                <transition name="fade">
                        <Error v-if="error != ''"/>
                </transition>

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
                state: ''
            }
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

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s ease-in-out;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

</style>