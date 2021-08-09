<template>
  <div class="page">

    <!-- JUMBOTRON -->
    <div class="home">
      <img src="../assets/img/gotta-catch-em-all-transparent-pokemon-logo-11.png" alt="">
    </div>

    <div class="container">
      <!-- SLIDERS for POKEMONS -->
      <vueper-slides
        fixed-height="250px"
        :bullets="false"
        class="no-shadow "
        :visible-slides="5"
        :dragging-distance="70">
        <vueper-slide v-for="pokemon in pokemons" :key="pokemon.id" :title="pokemon.name" :image="pokemon.img" />
  
      </vueper-slides>

      <!-- GRID LAYOUT for ARTICLES -->
      <div class="small-container">
        <GridLayout/>
      </div>

      <!-- SLIDERS for CARDS -->
      <CardSliders :array="cards"/>
    </div>

  </div>
</template>
<script>
import axios from 'axios';
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css';
import CardSliders from '@/components/CardSliders.vue';
import GridLayout from '@/components/GridLayout.vue'


export default {
  components: { VueperSlides, VueperSlide, CardSliders, GridLayout },
  
  data(){
    return{
      slides: [
        {
          title: 'pokemon.name',
        }
      ],
      url:'https://pokeapi.co/api/v2/pokemon/',
      urlCard:"https://api.pokemontcg.io/v2/cards?q=set.name:generations subtypes:ex",
      list_length:'',
      pokemons:[],
      pokemon:{},
      randNums:[],
      cards:[],
    }
  },

  mounted(){

    // Get the total number of cards through axios:list_length 
   axios
    .get(this.url)
    .then(response=>{
      this.list_length=response.data.count;
      console.log(this.list_length);

      // create an array(randNums) of 30 random Number from 1 to list_length
      while(this.randNums.length < 30){
        // create a random number
        const randNum = Math.floor(Math.random() * this.list_length) + 1;
        // push it into the array
        if(!this.randNums.includes(randNum)) {
        this.randNums.push(randNum);
        }
      }

      // For each random number generate an axios call to get all pokemons informations
      this.randNums.forEach(element => {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${element}`)
        .then(response=>{
          this.pokemon = {
              img:response.data.sprites.other['official-artwork'].front_default,
              id: response.data.id,
              name:response.data.name.charAt(0).toUpperCase() + response.data.name.slice(1).toLowerCase(),
          }
          if (!this.pokemons.includes(this.pokemon)) {
            this.pokemons.push(this.pokemon);
          }
        })
        
      });
                
    });
    

    // Axios call for generating an array of cards
    axios
    .get(this.urlCard)
    .then(response=>{
      this.cards=response.data.data;
      console.log(this.cards);
    });

  }

}

</script>

<style lang="scss" scoped>
.page{
  width:100%;
  overflow: hidden;

  .home{
    height: 600px;
    background-image: url('../assets/img/3693955.jpg');
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
  
    img{
      width: 400px;
    }
  }
    
  .vueperslide{
    background-color: #525252;
    background-size: contain;
    background-repeat:no-repeat ;
    cursor: pointer;
    color: transparent;
    font-size: 32px;
    z-index:4;

    &:hover{
      transform: scale(1.1);
      opacity: 0.6;
      color: whitesmoke;
      text-shadow: 
      3px 3px        black,
      2.75px 2.75px  black,
      2.5px 2.5px    black,
      2.25px 2.25px  black,
      2px 2px        black,
      1.75px 1.75px  black,
      1.5px 1.5px    black,
      1.25px 1.25px  black,
      1px 1px        black,
      0.75px 0.75px  black,
      0.5px 0.5px    black,
      0.25px 0.25px  black;
    }

  }
 
}

</style>
