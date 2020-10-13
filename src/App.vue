<template>
    <div id="app" class="body">
        <Carousel
            @next="next"
            @prev="prev"
        >
            <CarouselSlide v-for="(poke, index) in pokemons" 
                :key="index" 
                :index="index"
                :visibleSlide="visibleSlide"
                >
                <Pokemon :name="poke.name" :url="poke.url"/>
            </CarouselSlide>
        </Carousel>
    </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';
import Carousel from './components/Carousel';
import CarouselSlide from './components/CarouselSlide';

export default {
    name: 'App',
    data(){
        return{
            pokemons: [],
            visibleSlide: 0,
        }
    },
    created: function(){
        axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
            .then(res=>{
                //console.log(this.countSlides);
                this.pokemons = res.data.results;
            });
    },
    computed:{
        slidesLen(){
            return this.pokemons.length;
        }
    },
    methods:{
        next(){
            if (this.visibleSlide >= this.slidesLen - 1) {
                this.visibleSlide = 0;
            }else{
                this.visibleSlide ++;
            }
        },
        prev(){
            if (this.visibleSlide <= 0) {
                this.visibleSlide = this.slidesLen - 1;
            }else{
                this.visibleSlide --;
            }
        }
    },
    components:{
        Pokemon,
        Carousel,
        CarouselSlide
    }
}
</script>

<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .body{
        display: flex;
        justify-content: center;
        align-items: center;
        min-height: 100vh;
        width: 100%;
    }
</style>
