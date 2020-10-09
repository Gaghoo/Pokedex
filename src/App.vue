<template>
    <div id="app">
        <div class="column is-one-third is-offset-one-third">
            <div v-for="(poke, index) in pokemons" :key="index">
            <Pokemon :name="poke.name" :url="poke.url"/>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';


export default {
    name: 'App',
    data(){
        return{
            pokemons: []
        }
    },
    created: function(){
        axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then(res=>{
                //console.log("Pegou os pokemons da primeira geração");
                this.pokemons = res.data.results;
            });
    },
    components:{
        Pokemon
    }
}
</script>

<style>

</style>
