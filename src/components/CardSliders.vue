<template>

<section>

    <button><router-link :to="{name: 'GCCPokemon'}"><span>See all the cards</span></router-link></button>

    <vueper-slides
    fixed-height="290px"
    :bullets="false"
    class="no-shadow card-wrapper"
    :visible-slides="6"
    :gap="1"
    :dragging-distance="70">
        <vueper-slide v-for="item in array" :key="item.id" :image="item.images['small']" />
    </vueper-slides>

</section>

</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'
export default {
    name:'CardSliders',
    components: { VueperSlides, VueperSlide },
    props:{
        array:Array
    },

    methods:{
        see(){
            console.log(this.array);
        }
    }

}
</script>

<style lang="scss" scoped>

button{
    background-color: #525252;
    border:2px solid #525252;

    a{
        display: inline-block;
        color:white;
        text-decoration: none;
        font-weight: 500;
        font-size: 18px;
        padding: 10px 20px;
    }
}

.card-wrapper{
    margin:0;
    padding: 20px 0;
    background-color: #525252;
}

</style>