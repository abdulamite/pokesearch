<template>
    <div>
        <div v-if="pokemon.id != undefined" class="card">
            <div class="pokemon-img">
                <img  :src="getSprite" :alt="pokemon.id" />
            </div>  
            <div class="pokemon-info">
                <h1 id="pokemon-name"> {{ pokemonName }} </h1>
                <Types v-bind:types="pokemon.types"/>
                <h2>Abilities</h2>
                <p v-for="power in pokemon.abilities" class="abilities" >{{ ((power.ability.name).charAt(0).toUpperCase() + power.ability.name.slice(1)) }}</p>
                <Stats v-bind:stats="pokemon.stats"/> 
            </div>
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
    height: 150px;
    width:auto;
}

.pokemon-img{
    transition: cubic-bezier(0.075, 0.82, 0.165, 1) .3s;
    margin: 1em;
}

.abilities{
    margin:.5rem;
}

.pokemon-img:hover{
    transition: cubic-bezier(0.075, 0.82, 0.165, 1) .3s;
    transform: scale(1.15);
}


.card{
    height: 100%;
    background:white;
    padding:2rem;
    overflow-y: scroll;
}

#pokemon-name{
    font-family: 'DM Serif Display', serif
}


</style>