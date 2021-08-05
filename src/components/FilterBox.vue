<template>
<section class="container">
    <div class="search">
        <div class="small-container">
            <div class="top-filter-box">
                <div class="left">
                    <h2>Nome o Numero</h2>
                    <input type="text">
                </div>
                <div class="right">
                    <h3>Cerca un Pokémon per nome o per numero del Pokédex Nazionale</h3>
                </div>
            </div>

            <h4>Usa la ricerca avanzata per trovare Pokémon in base al tipo, all'abilità e altro ancora!</h4>
        
        </div> 

    </div>
    <div class="advanced-search">
        <div class="small-container" >

            <div class="types">
                <button :class="item" v-for="(item,index) in typeArray" :key="index">{{item}}</button>
            </div>
         
        </div> 


    </div>
    
</section>
</template>

<script>
import listTypePokedex from '@/data/listTypePokedex.js';



export default {
    name: 'FilterBox',
    data(){
        return{
            typeArray:listTypePokedex,
        }
    }
}
</script>

<style lang="scss" scoped>
section{
    .search{
        background-color: #313131;
        width: 100%;
    
        .small-container{
    
            .top-filter-box{
                padding: 30px 0;
                display: flex;
                align-items: center;
                justify-content: space-between;
        
                .right{
                    width: calc(100% / 2);
                    color:#fff;
                    background-color: #4dad5b;
                    border-radius:5px;
                    padding:  15px;
                }
            }
    
        }
    
    }
    
    .advanced-search{
        background-color: #616161;
        width: 100%;

        .small-container{

            .types{
                width:calc(100% / 2);
                display: flex;
                flex-flow: row wrap;

              button{
                  width: 120px;
                  margin: 5px 40px;
                  text-align: center;
                  padding: 6px 0;
                  border-radius: 5px;
                }


            }

        }

       
    }

}

</style>