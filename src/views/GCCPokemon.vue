<template>
  <div class="page">

    <div class="container">

      <div class="small-container">
        <h2>GCC POKÉMON</h2>
      </div>

      <div class="select">

        <div class="select-container">

          <div class="message">
            <h3>Scegli il Subtype per la ricerca delle Cards</h3>
          </div>

          <div class="all-subtypes">
            <button @change="showCard" class="btn-grad "> 
              <input class="hide " type="radio" id="normal" value="Normal" v-model="checkedNames">
              <label for="normal">Normal</label>
            </button>

            <button v-for="(item,index) in subtypes" :key="index" @change="showCard" class="btn-grad ">     
              <input class="hide " type="radio" :id="index" :value="item" v-model="checkedNames">
              <label :for="index">{{item}}</label>
            </button>
          </div>

        </div>

      </div>

      <FilterCards @changeType="receivedType" @changeRarity="receivedRarity" @sendWord="receivedSearch"/>
      

      <div class="all-cards">
        <div class="reset">
          <button @click="reset">reset</button>
        </div>
        <Card  v-for="card in filteredCards" :key="card.id" :details="card"/>
      </div>

    </div>

  </div>
</template>

<script>
import axios from 'axios';
import Card from '@/components/Card.vue';
import FilterCards from '@/components/FilterCards.vue';


export default {
  components:{
    Card,
    FilterCards
  },
  data(){
    return{
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
      cards:[],
      checkedNames:'',
      selectRarity:'',
      selectType:'',
      search:''
    }
  },

  computed : {
    filteredCards : function (){
      return this.filterByWord(this.filterByType(this.filterByRarity(this.cards)));
    }
  },


  methods:{

    // method that show the card based on the subtypes choosen
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

    // method that assaign the V-model rarity send through emit at selectRarity
    receivedRarity(arg1){
      this.selectRarity = arg1;
    },

    // method that assaign the V-model type send through emit at selectType
    receivedType(arg2){
      this.selectType = arg2;
    },

    // method that assaign the V-model searchWord send through emit at search
    receivedSearch(arg3){
      this.search = arg3;
    },

    // method that filter the cards based on rarity
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

    // method that filter the cards based on type
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

    // method that filter the cards based on word searched
    filterByWord(array){
      return array.filter((element)=>{
        return element.name.toLowerCase().match(this.search.toLowerCase())
      });
    },

    // method to reset all filters
    reset(){
      this.selectRarity ='';
      this.selectType = '';
      this.search = '';
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

    .select{
      background-color: #616161;

      .select-container{
        padding-top: 30px;
        width: 70%;
        margin:0 auto;

        .message{
          width: calc(100% / 2);
          text-align: center;
          color:#fff;
          background-color: #4dad5b;
          border-radius:5px;
          padding:  10px;
        }

        .all-subtypes{
          display: flex;
          flex-flow: row wrap;
          padding: 20px 0;
         
         .btn-grad {background-image: linear-gradient(to right, #ECE9E6 0%, #FFFFFF  51%, #ECE9E6  100%)}
         .btn-grad {
            margin: 10px;
            padding: 10px 20px;
            text-align: center;
            text-transform: uppercase;
            transition: 0.5s;
            background-size: 200% auto;
            color: gray;            
            box-shadow: 0 0 5px #eee;
            border-radius: 10px;
            display: block;
            label{
              font-weight: 500;}

            input.hide{
              display: none;
            }
          }

          .btn-grad:hover {
            background-position: right center; /* change the direction of the change here */
            color: #313131;
            text-decoration: none;
          }
        }
      }
    }

    .all-cards {
      min-height: 200px;
      background-color: #fff;
      width: 70%;
      margin:0 auto;
      display: flex;
      flex-flow: row wrap;

      .reset{
        width: 100%;
        padding: 20px 20px 15px 0;
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
    }
  }
}

</style>