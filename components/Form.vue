<template>
    <div>
        <Header />
        <PokemonCard v-bind:pokemon="pokemon"/>  
            <el-input id="search" placeholder="Pokemon Name" v-model="search" @keyup.enter.native="fetchData" clearable ></el-input>
            <el-button @click="fetchData">Get Pokémon</el-button>
              <transition name="fade">
                    <Error v-if="error != ''"/>
              </transition>
            
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
                    const pokemon = await P.getPokemonByName(this.search.toLowerCase())
                    .then(function(response) {
                    return response;
                    });
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

* {
    margin-top: 1em;
    margin-bottom: 1em;
}

.el-input__inner{
    border:red;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    transform: translateY(-100);
    transition: all .3s ease-in-out;
}

</style>