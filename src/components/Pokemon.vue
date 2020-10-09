<template>
<div id="pokeCard">
    <div class="card">
        <div class="card-image">
            <figure class="image is-square">
            <img :src="pokemon.icon" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-left">
                <figure class="image is-96x96">
                <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="media-content">
                <p class="title is-4">{{upperName}}</p>
                <p class="subtitle is-6">{{pokemon.type}}</p>
            </div>
            </div>

            <div class="content">
                <button class="button is-success is-outlined" @click="backToFront">Mudar icone</button>
                <br>
                <time datetime="2016-1-1">11:09 PM - 1 Jan 2016</time>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.icon = res.data.sprites.other.dream_world.front_default;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front
            console.log(res.data.types)
        })
    },
    data(){
        return{
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                icon: '',
                front: '',
                back: ''
            }
        }
    },
    props:{
        name: String,
        url: String
    },
    computed:{
        upperName(){
            return this.name[0].toUpperCase() + this.name.slice(1)
        }
    },
    methods:{
        backToFront: function(){
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else{
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style>
    #pokeCard{
        margin: 10px;
    }
</style>