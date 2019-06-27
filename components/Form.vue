<template>
    <div>
        <Header />
        <div class="split-container">
            <div class="form-container">
                <h1>Search for a Pokémon!</h1>
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
                error: ''
            }
        },
        methods:{
            fetchData:async function(){
                if (this.search === ''){

                }
                try{
                    const pokemon = await P.getPokemonByName(this.search.toLowerCase().replace(/(^\s+|\s+$)/g,''))
                    .then(function(response) {
                    return response;
                    });
                    console.log(pokemon)
                    this.error = '';
                    this.pokemon = pokemon;
                    
                }catch(e){
                    this.error = e;
                }
            }
        }

    }
</script>

<style scoped>
.split-container{
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: space-between;
}

.split-container>*{
    width:50vw;
    height: 100vh;
    padding:3rem;
}

#pokemon-container{
    background-size: cover;
    background-position: center;
    overflow: hidden;
    overflow-y: scroll;
}

.form-container{

}

.form-container>*{
    margin:1rem;
}

.el-input{
    width: 75%;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    transform: translateY(-100);
    transition: all .3s ease-in-out;
}

</style>