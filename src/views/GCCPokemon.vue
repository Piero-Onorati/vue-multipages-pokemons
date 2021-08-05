<template>
  <section>
    <h2>all the cards</h2>

  <button @change="showCard"> 
      <input class="hide" type="radio" id="normal" value="Normal" v-model="checkedNames">
      <label for="normal">Normal</label>
  </button>
  
  <button v-for="(item,index) in subtypes" :key="index" @change="showCard">     
      <input class="hide" type="radio" :id="index" :value="item" v-model="checkedNames">
      <label :for="index">{{item}}</label>
  </button>

  <span>Checked names: {{ checkedNames }}</span>

  <div class="all-filters">

  <select v-model="selectRarity">
      <option value="All">All</option>
      <option  v-for="(rarity,index) in rarities" :key="'b'+ index">{{rarity}}</option>
  </select>
  <span>Checked names: {{ selectRarity}}</span>

  <input type="text" placeholder="Search a card..." v-model="search">

  <select  v-model="selectType">
      <option value="All">All</option>
      <option v-for="(type,index) in types" :key="'c'+ index">{{type}}</option>
  </select>

  <span>Checked names: {{selectType}}</span>
  </div>

  <div class="all-cards">
  
    <div v-for="card in filteredCards" :key="card.id" class="card">
        <img :src="card.images['small']" alt="">
        <h3>{{card.name}}</h3>
        <h4>{{card.rarity}}</h4>
        <h4 v-for="(item,index) in card.types" :key="'e'+ index">{{item}}</h4>
        <h4>{{card.supertype}}</h4>
    </div>
  
  </div>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return{
      checkedNames:'',
      cards:[],
      subtypes:[
          "Baby",
          "Basic",
          "EX",
          "GX",
          "Goldenrod&Game&Corner",
          "Item",
          "Level-Up",
          "MEGA",
          "Pokémon&Tool",
          "Pokémon&Tool&F",
          "Rapid&Strike",
          "Restored",
          "Rocket's&Secret&Machine",
          "Single&Strike",
          "Special",
          "Stadium",
          "Stage&1",
          "Supporter",
          "TAG&TEAM",
          "Technical&Machine",
          "V",
          "VMAX"
      ],
      search:'',
      rarities:[],
      selectRarity:'',
      URLRarities:"https://api.pokemontcg.io/v2/rarities",
      URLTypes:"https://api.pokemontcg.io/v2/types",
      selectType:'',
      types:[]

    }
  },

  computed : {
    filteredCards : function (){
        return this.filterByWord(this.filterByType(this.filterByRarity(this.cards)));
    }
  },

  mounted(){
    axios
      .get(this.URLRarities)
      .then(response=>{
          console.log(response.data.data);
          this.rarities=response.data.data
          console.log(this.rarities);
      });

    axios
    .get(this.URLTypes)
    .then(response=>{
      console.log(response.data.data);
      this.types=response.data.data
      console.log(this.types);
    });
    
  },

  methods:{
    showCard(){
        if (this.checkedNames =='Normal') {
            axios
                .get("https://api.pokemontcg.io/v2/cards")
                .then(response=>{
                    console.log(response.data.data);
                    this.cards=response.data.data;
                    console.log(this.cards); 
                });
                this.selectRarity='';
                this.selectType='';

            
        }else{

            axios
                .get(`https://api.pokemontcg.io/v2/cards?q=subtypes:${this.checkedNames}&orderBy=-set.releaseDate`)
                .then(response=>{
                    console.log(response.data.data);
                    this.cards=response.data.data
                    console.log(this.cards);
                });
                this.selectRarity='';
                this.selectType='';
        }
    
    },

    filterByRarity(array){
        return array.filter(element =>{
            if (this.selectRarity == '' || this.selectRarity == 'All') {
                return array
            }
            else{
                return element.rarity == this.selectRarity
            }
            
        });
    },

    filterByType(array){
        return array.filter(element =>{
            const set1 = new Set(element.types);
            if (set1.has(this.selectType)) {
              return element
            }else if(this.selectType ==''|| this.selectType =='All'){
              return array
            }
        });
    },

    filterByWord(array){
      return array.filter((element)=>{
        return element.name.toLowerCase().match(this.search.toLowerCase())
      });
    }

  }


}
</script>

<style lang="scss" scoped>

section{
  padding-top:100px;

   .all-cards{
      background-color: tomato;
      width:75%;
      margin: 0 auto;
      display: flex;
      flex-flow: row wrap;
      .card{
        margin: 0 10px;
        width: calc((100% / 5) - 20px);

        img{
          width:100%;
        }
          
      }

    
    }

    .all-filters{
      background-color: bisque;
      padding: 50px 0;
      width:100%;
      display: flex;
      align-items: center;
      justify-content: space-around;

      
      input.hide{
          display: none;
      }

      button{
          padding: 5px 10px;
          margin:10px
      }

    }

}







</style>