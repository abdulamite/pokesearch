<template>
    <div>
        <div v-if="pokemon.id != undefined" class="card">
            <img  :src="getSprite" :alt="pokemon.id" />
            <h1> {{ pokemonName }} </h1>
            <Types v-bind:types="pokemon.types"/>
            <h2>Abilities</h2>
            <p v-for="power in pokemon.abilities" >{{ ((power.ability.name).charAt(0).toUpperCase() + power.ability.name.slice(1)) }}</p>
            <Stats v-bind:stats="pokemon.stats"/> 
        </div>
    </div>
</template>

<script>
import Types from '~/components/Types.vue'
import Stats from '~/components/Stats.vue'
const Pokedex = require('pokeapi-js-wrapper');
const P = new Pokedex.Pokedex();

    export default {
        components:{
            Types,
            Stats
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
    height: 235px;
    width:auto;
}

.card{
    padding:1rem;
}


</style>