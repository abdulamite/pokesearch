<template>
    <div>
        <div v-if="pokemon.id != undefined" class="card">
            <img  :src="getSprite" :alt="pokemon.id" />
            <h1> {{ pokemonName }} </h1>
            <Types v-bind:types="pokemon.types"/>
            <p v-for="power in pokemon.abilities" >{{ power.ability.name }}</p>
        </div>
        <h1 v-else>Search for a Pokémon!</h1>
    </div>
</template>

<script>
import Types from '~/components/Types.vue'
const Pokedex = require('pokeapi-js-wrapper');
const P = new Pokedex.Pokedex();

    export default {
        components:{
            Types
        },
        props: ['pokemon'],
        computed:{
            getSprite:function () {
                return `https://img.pokemondb.net/artwork/${this.pokemon.name}.jpg`
            },
            pokemonName:function(){
                const name = this.pokemon.name.split('');
                name[0] = name[0].toUpperCase();
                return name.join('');
            }
        }

    }
</script>

<style scoped>
img{
    height: 150px;
    width:auto;
}


.types{
    display: flex;
    justify-content: center;
    margin:.5rem;
}

.types>p{
    margin:.3rem;
    padding:.5rem;
    border-radius: .2rem;
}

.rock{
    background-color:#bcaaa4;
}

.ground{
    background-color:#a1887f;
}

.electric{
    background-color:#fff176;
}


</style>