<template>
   <div class="all-filters">

        <div class="small-container">

          <div class="all-subtypes">
            <select v-model="rarity" @change="$emit('changeRarity', rarity)">
              <option value="All">All</option>
              <option  v-for="(rarity,index) in rarities" :key="'b'+ index">{{rarity}}</option>
            </select>
          </div>


          <div class="search-word">
            <input type="text" placeholder="Search a card..." v-model="searchWord">
            <button @click="$emit('sendWord', searchWord)">Search</button>
          </div>

          <select  v-model="type" @change="$emit('changeType', type)">
            <option value="All">All</option>
            <option v-for="(type,index) in types" :key="'c'+ index">{{type}}</option>
          </select>

        </div>

      </div>
</template>

<script>
import axios from 'axios';

export default {
  data(){
    return{
      searchWord:'',
      rarities:[],
      type:'',
      rarity:'',
      URLRarities:"https://api.pokemontcg.io/v2/rarities",
      URLTypes:"https://api.pokemontcg.io/v2/types",
      types:[]
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

 

}
</script>

<style lang="scss" scoped>

.all-filters{
      background-color: #313131;
      padding: 50px 0;
      width:100%;

      .small-container{
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