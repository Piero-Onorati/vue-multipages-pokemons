<template>
<div class="page">

  <!-- Title -->
  <div class="container">
    <div class="small-container">
      <h2>Pokédex</h2>
    </div>
  </div>

  <!-- FilterBox for Pokémpn -->
  <FilterBox @choseType="receivedType" @sendSearchPoke="receivedSearchPoke"  @sendHeight="receivedHeight" @sendWeight="receivedWeight"/>

  <!-- All Pokemons Box -->
  <div class="container">
    <div class="all-pokemon" v-if="!loading">

      <!-- 'Reset all filters' button -->
      <div class="reset">
        <button @click="reset">reset</button>
      </div>

      <!-- Pokemon Card component -->
      <div v-for="pokemon in filteredPokemons" :key="pokemon.id" class="pokemon">
        <PokeCard :pokemon="pokemon" />
      </div>

    </div>

    <!-- Loader -->
    <Loader v-else/>
  </div>

</div>
  
</template>

<script>
import axios from 'axios';
import FilterBox from '@/components/FilterBox.vue';
import PokeCard from '@/components/PokeCard.vue';
import Loader from '@/components/Loader.vue';

export default {
  name: 'Pokedex',
  components: {
  FilterBox,
  PokeCard,
  Loader
  },
  data(){
    return{
      url:'https://pokeapi.co/api/v2/pokemon/',
      list_length:'',
      pokemon:{},
      pokemons:[],
      selectedType:'',
      selectedPoke:'',
      selectedHeight:'',
      selectedWeight:'',
      loading:true
    }
  },

  computed : {
    filteredPokemons : function (){
      return this.filterByWord(this.filterByType(this.filterByHeight(this.filterByWeight(this.pokemons))));
    }
  },

  mounted(){
    axios
    .get(this.url)
    .then(response=>{
      this.list_length=response.data.count;
      console.log(this.list_length);

      // Generate Pokedex
      for (let index = 1; index <= this.list_length; index++) {
        axios
        .get(`https://pokeapi.co/api/v2/pokemon/${index}`)
        .then(response=>{
          this.pokemon = {
            image: response.data.sprites['front_default'],
            img:response.data.sprites.other['official-artwork'].front_default,
            id: response.data.id,
            name:response.data.name.charAt(0).toUpperCase() + response.data.name.slice(1).toLowerCase(),
            type:response.data.types.map(element=>{
              return element.type['name'].toUpperCase()
            }),
            abilities:response.data.abilities.map(element=>{
              return element.ability['name']
              }),
            move:response.data.moves[0].move.name,
            stats:response.data.stats.map(element=>{
              return element.stat.name
            }),
            stats_number:response.data.stats.map(element=>{
              return element.base_stat
            }),
            height:response.data.height,
            weight:response.data.weight,
          }
          console.log(this.pokemon);  
            
        })
        .catch(error=>{
          console.log(error)
        })
        .finally(()=>{
          if (!this.pokemons.includes(this.pokemon)) {
            this.pokemons.push(this.pokemon);
          }
          this.loading=false;
        });
          
      }
                
    })
                  
  },

  methods:{

    // method that assaign the V-model checkedType send through emit at selectedType
    receivedType(arg1){
      this.selectedType = arg1;
    },

    // method that assaign the V-model searchPoke send through emit at selectedPoke
    receivedSearchPoke(arg2){
      this.selectedPoke = arg2;
    },
    // method that assaign the V-model selectedHeight send through emit at pickedHeight
    receivedHeight(arg3){
      this.selectedHeight=arg3;
    },

    // method that assaign the V-model selectedWeight send through emit at pickedWeight
    receivedWeight(arg4){
      this.selectedWeight=arg4;
    },

    // method that filter the cards based on word searched
    filterByWord(array){
      return array.filter((element)=>{
        if (this.selectedPoke != '') {
          if (!isNaN(this.selectedPoke)) {
            return element.id == this.selectedPoke
          }else{
            return element.name.toLowerCase().match(this.selectedPoke.toLowerCase());
          }
        } else{
          return array
        }
      })
    },

    // method that filter the cards based on type
    filterByType(array){
      return array.filter(element =>{
      const set1 = new Set(element.type);
      if (set1.has(this.selectedType)) {
        return element
      }else if(this.selectedType ==''){
        return array
      }

      }); 
    },

    // method that filter the cards based on height
    filterByHeight(array){
      return array.filter(element =>{
        if (this.selectedHeight=='')  {
          return array 
        }else {
          return element.height < parseInt(this.selectedHeight )           
        }
      })

    },

    // method that filter the cards based on weight
    filterByWeight(array){
      return array.filter(element =>{
        if (this.selectedWeight=='')  {
          return array 
        }else {
          return element.weight < parseInt(this.selectedWeight )           
        }
      })

    },

    // method to reset all filters
    reset(){
      this.selectedType ='';
      this.selectedPoke = '';
      this.selectedHeight = '';
      this.selectedWeight = '';
    }
  }

}

</script>

<style lang="scss" scoped>

.page{

  .container{

    .small-container{
      padding-top: 130px;
      background-color: #ffffff;

      h2{
        font-size: 30px;
        font-weight:400;
        padding-bottom: 10px;
        color:#919191;
      }
    }
  }

  .container{

      
    .all-pokemon {
      background-color: #fff;
      width: 70%;
      margin:0 auto;
      display: flex;
      flex-flow: row wrap;

      .reset{
        width: 100%;
        padding: 20px 10px 15px 0;
        text-align: right;

        button{
          background-color: #30a7d7;
          color:white;
          padding: 5px 20px;
          border-radius:5px;
          text-transform: uppercase;
          font-size: 18px;
          border: none;
          cursor: pointer;
        }
        
      }

      .pokemon{
        width: calc((100% / 4) - 20px);
        margin:10px;
      }

    }

    
  }

}



</style>
