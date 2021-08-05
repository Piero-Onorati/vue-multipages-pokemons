<template>
<div class="page">
  <div class="container">
    <div class="small-container">
      <h2>Pokédex</h2>
    </div>
  </div>
  <FilterBox/>
  <div class="container">
    <div class="all-pokemon">
      <div v-for="pokemon in pokemons" :key="pokemon.id" class="pokemon">
        <PokeCard :pokemon="pokemon"/>
      </div>
    </div>
  </div>

</div>
  
</template>

<script>
import axios from 'axios';
import FilterBox from '@/components/FilterBox.vue';
import PokeCard from '@/components/PokeCard.vue';

export default {
    name: 'Pokedex',
    components: {
    FilterBox,
    PokeCard
    },
    data(){
      return{
        url:'https://pokeapi.co/api/v2/pokemon/',
        list_length:'',
        pokemon:{},
        pokemons:[],
      }
    },

    mounted(){
      axios
      .get(this.url)
      .then(response=>{
        this.list_length=response.data.count;

        console.log(this.list_length);
        for (let index = 1; index <=  this.list_length; index++) {

            axios
            .get(`https://pokeapi.co/api/v2/pokemon/${index}`)
            .then(response=>{
              this.pokemon = {
                  image: response.data.sprites['front_default'],
                  id: response.data.id,
                  name:response.data.name.charAt(0).toUpperCase() + response.data.name.slice(1).toLowerCase(),
                  type:response.data.types.map(element=>{
                    return element.type['name'].toUpperCase()
                  }),
                  abilities:response.data.abilities.map(element=>{
                    return element.ability['name']
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
            });
            
        }
                  
      })
                   
    }

}

</script>

<style lang="scss" scoped>

.page{
  width: 100%;
  min-height: 100vh;
  background-color: #313131;
  background: repeating-linear-gradient( -45deg, #2f2f2f, #2f2f2f 11px, #313131 11px, #313131 55px );

  .container{
    background-color: #ffffff;
    background: repeating-linear-gradient( -45deg, #f5f5f5, #f5f5f5 11px, #ffffff 11px, #ffffff 55px );

    .small-container{
      padding-top: 100px;
      background-color: #ffffff;
    }
  }

  .container{

      
    .all-pokemon {
      background-color: #fff;
      width: 70%;
      margin:0 auto;
      display: flex;
      flex-flow: row wrap;

      .pokemon{
        width: calc((100% / 4) - 20px);
        margin:10px;
      }

    }

    
  }

}



</style>
