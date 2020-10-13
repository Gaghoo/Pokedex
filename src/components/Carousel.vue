<template>
    <div class="carousel">
        <slot></slot>
        <button class="next" @click="next">Next</button>
        <button class="prev" @click="prev">Prev</button>
    </div>
</template>

<script>
export default {
    data(){
        return{

        }
    },
    methods:{
        next() {
            this.$emit('next');
        },
        prev() {
            this.$emit('prev');
        }
    }
}
</script>

<style>
    .carousel{
        position: relative;
    }
    button{
        position: absolute;
        height: 40px;
        width: 50px;
        top: calc(50% - 20px);
        background-color: rgba(0, 0, 0, 0.6);
        border: none;
        color: aliceblue;
    }
    button:focus, button:hover{
        outline: none;
        cursor: pointer;
    }
    .next{
        right: 0;
        border-radius: 10px 0px 0px 10px ;
    }
    .prev{
        left: 0;
        border-radius: 0px 10px 10px 0px ;
    }
</style>