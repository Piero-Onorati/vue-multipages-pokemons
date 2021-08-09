<template>
  <div class="all-filters">

    <div class="small-container">
      
      <!-- Filter Card with rarity -->
      <div class="all-rarities">
        <select v-model="rarity" @change="$emit('changeRarity', rarity)">
          <option value="All">All</option>
          <option  v-for="(rarity,index) in rarities" :key="'b'+ index">{{rarity}}</option>
        </select>
      </div>

      <!-- Search Card by name box -->
      <div class="search-word">
        <input type="text" placeholder="Search a card..." v-model="searchWord">
        <button @click="submit">Search</button>
      </div>

      <!-- Filter Card with type -->
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

  methods:{
    submit(){
      this.$emit('sendWord', this.searchWord);
      this.searchWord='';
    }
  }

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
      margin:10px;

    }

    select{
      border: 1px solid lightgray;
      background-color: #333;
      color: lightgray;
      padding: 10px;
      outline: none;
      font-size: 1em;
      border-radius: 3px;
      transition: width .3s;
      option{
        font-family: "Exo";
      }
    }

    .search-word{

      input{
        padding: 8px;
        outline: none;
        border:none;
        font-size: 1em;
        border-radius: 3px;
      }

      button{
        background-color: #ee6b2f;
        color: white;
        margin-left: 10px;
        border:none;
        padding: 8px;
        outline: none;
        font-size: 1em;
        border-radius: 3px;

      }
    }

  }
}


</style>