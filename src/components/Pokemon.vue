<template>
    <div id="pokeCard" class="card">
        <div class="content">
            <h3>#{{this.pokemon.id}} - {{upperName}}</h3>
            <span v-for="(types, index) in pokemon.types" :key="index"> {{types.type.name.toUpperCase()}} </span><br>
        </div>
        <img :src="pokemon.icon" :alt="name">
    </div>
<!--<h6 v-for="(type, index) in pokemon.types" :key="index">{{type.type.name}}</h6>-->
</template>

<script>
import axios from 'axios';

export default {
    created: function(){
        axios.get(this.url).then(res =>{
            this.pokemon.types = res.data.types;
            this.pokemon.icon = res.data.sprites.other.['official-artwork'].front_default;
            this.pokemon.id = res.data.id;
            this.pokemon.height = res.data.height;
            //console.log(res.data.sprites.other)
        })
    },
    data(){
        return{
            isFront: true,
            currentImg: '',
            pokemon: {
                types: [],
                icon: '',
                front: '',
                back: '',
                id: '',
                height:''
            },
            typesColor: {
                grass: "#9bcc50",
                poison: "#b97fc9",
                fire: "#fd7d24",
                psychic: "#f366b9",
                flying: ["#3dc7ef","#bdb9b8"],
                ice: "#51c4e7",
                water: "#4592c4",
                ground: ["#f7de3f","#ab9842"],
                rock: "#a38c21",
                electric: "#eed535",
                bug: "#729f3f",
                normal: "#a4acaf",
                fighting: "#d56723",
                fairy: "#fdb9e9",
                steel: "#9eb7b8",
                ghost: "#7b62a3",
                dragon: ["#53a4cf", "#f16e57"],
                dark: "#707070"
            },
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
        },
        
    }
}
</script>

<style>
    .card{
        position: relative;
        width: 500px;
        height: 250px;
        margin: 20px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
        border-radius: 30px;
        background: linear-gradient(135deg, #9bcc50, #b97fc9);
    }
    .card img{
        position: absolute;
        bottom: 0;
        left: 50%;
        transform: translateX(-50%);
        height: 200px;
        transition: 500ms;
    }
    .card:hover img{
        height: 350px;
        left: 80%;
    }
    .card .content{
        position: relative;
        width: 50%;
        left: 20%;
        padding: 20px 20px 20px 40px;
        opacity: 0;
        visibility: hidden;
        transition: 500ms;
    }
    .card .content h3{
        font-family: Arial, Helvetica, sans-serif;
        font-size: 25px;
        font-weight: bold;
        color: #fff;
        text-shadow: 2px 4px 9px #677;
    }
    .card .content span{
        display: block;
        margin: 5px 10px;
        padding: 8px 5px;
        border: 1px solid #000;
        border-radius: 15px;
        text-align: center;
        font-weight: bold;
    }
    .card .content a{
        position: relative;
        display: inline-block;
        color:  #111;
        padding: 10px 20px;
        font-family: Arial, Helvetica, sans-serif;
        font-weight: bold;
        border-radius: 10px;
        background-color: #ccc;
        text-decoration: none;
    }
    .card:hover .content{
        left: 0;
        opacity: 1;
        visibility: visible;
    }
</style>