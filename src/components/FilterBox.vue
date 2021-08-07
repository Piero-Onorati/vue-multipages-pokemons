<template>
<section class="container">

    <!-- SEARCH part: contains the input text + button for searching name/numbers of pokemon  -->
    <div class="search">
        <div class="small-container">
            <div class="top-filter-box">
                <div class="left">
                    <h2>Nome o Numero</h2>
                    <input type="text" v-model="searchPoke" placeholder="Search a Pokémon...">
                    <button @click="submit">Search</button>
                    
                </div>
                <div class="right">
                    <h3>Cerca un Pokémon per nome o per numero del Pokédex Nazionale</h3>
                </div>
            </div>

            <h4>Usa la ricerca avanzata per trovare Pokémon in base al tipo ed altro ancora!</h4>
        
        </div> 

    </div>

    <!-- ADVANCED-SEARCH part: contains the filter for TYPE, HEIGHT and WEIGHT of pokemon (+ the buttons for opening/closing of the advanced-search part itself) -->
    <div class="advanced-search">

        <!-- ADVANCED-SEARCH container -->
        <div class="advanced-container" v-if="expand">
            
            <!-- TYPES: buttons for selecting different pokemon typt(grass, water, fire, etc.) -->
            <div class="types">
                <button :class="item" v-for="(item,index) in typeArray" :key="'a'+ index" @change="$emit('choseType',checkedType)">
                    <input type="radio" :id="'a' + index" :value="item" v-model="checkedType">
                    <label :for="'a' + index">{{item}}</label>
                </button>
            </div>

            <!-- ALL FILTERS: 3 Buttons for different heights + 3 Buttons for different weights -->
            <div class="all-fiters">

                <!-- Buttons for different heights -->
                <div class="height">
                    <h2>Altezza</h2>
                    <div class="all-buttons-height" @change="$emit('sendHeight', pickedHeight)">
                        <button class="height-item" >
                            <input type="radio" id="one" value="10" v-model="pickedHeight" >
                            <label for="one"><img src="../assets/img/002_Ivysaur_icon-icons.com_67333.png" alt="ivysaur"></label>
                        </button>
                        <button class="height-item">
                            <input type="radio" id="two" value="20" v-model="pickedHeight" >
                            <label for="two"><img src="../assets/img/Milotic_icon-icons.com_67385.png" alt="milotic"></label>
                        </button>
                        <button class="height-item">
                            <input type="radio" id="three" value="50" v-model="pickedHeight" >
                            <label for="three"><img src="../assets/img/Rayquaza_icon-icons.com_67460.png" alt="rayquaza"></label>
                        </button>
                    </div>
                </div>

                <!-- 3 Buttons for different weights -->
                <div class="weight">
                    <h2>Peso</h2>
                    <div class="all-buttons-weight" @change="$emit('sendWeight', pickedWeight)">
                        <button class="weight-item">
                            <input type="radio" id="four" value="100" v-model="pickedWeight">
                            <label for="four"><img src="../assets/img/036_Pichu_icon-icons.com_67298.png" alt="pichu"></label>
                        </button>
                        <button class="weight-item">
                            <input type="radio" id="five" value="500" v-model="pickedWeight">
                            <label for="five"><img src="../assets/img/009_Blastoise_icon-icons.com_67326.png" alt="blaistoise"></label>
                        </button>
                        <button class="weight-item">
                            <input type="radio" id="six" value="1000" v-model="pickedWeight">
                            <label for="six"><img src="../assets/img/Snorlax_icon-icons.com_67365.png" alt="snorlax"></label>
                        </button>
                    </div>
                </div>

            </div>
         
        </div> 

        <!-- ADVANCED-SEARCH buttons: EXPAND/CLOSE -->
        <div class="expand">
        <div class="btn-container">
            <button @click="expand=true" v-if="!expand">Ricerca avanzata</button>
            <button @click="expand=false" v-else>close</button>
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
            pickedHeight:'',
            pickedWeight:'',
            expand:false,
            checkedType:'',
            searchPoke:'',
        }
    },
    methods:{
        submit(){
        this.$emit('sendSearchPoke',this.searchPoke);
        this.searchPoke ='';
    }
  }
}
</script>

<style lang="scss" scoped>
section{
    .search{
        background-color:#313131;
        width: 100%;
        padding-bottom: 20px;
    
        .small-container{
    
            .top-filter-box{
                padding: 30px 0;
                display: flex;
                align-items: center;
                justify-content: space-between;

                .left{
                    h2{
                        color: white;
                        font-weight:300;
                        padding-bottom:5px;
                    }

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
        
                .right{
                    width: calc(100% / 2);
                    color:#fff;
                    background-color: #4dad5b;
                    border-radius:5px;
                    padding:  15px;
                }
            }

            h4{
                color: white;
                font-weight: 300;
            }
        }
    }
    
    .advanced-search{
        background-color: #616161;
        width: 100%;

        .advanced-container{
            display: flex;
            padding: 30px 0 50px 0;
            width: 70%;
            margin:0 auto;

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

                  input{
                      display: none;
                  }
                }
            }

            .all-fiters{
                height: 100px;
                width:calc(100% / 2);
                display: flex;
                flex-direction: column;
                align-items: center;

                .height{
                    margin-bottom: 40px;

                    h2{
                        color: white;
                        font-weight: 400;
                        padding-bottom: 10px;
                        padding-left: 10px;
                    }
                    .all-buttons-height{
                        .height-item{
                            margin: 0 10px;

                            input{
                                display: none;
                            }
                            label{
                                display: inline-block;
                                padding: 20px;
                                
                                img{
                                    width: 70px;
                                   filter: brightness(0)  grayscale(100%);  
                                }
                            }
                        }
                    }

                }

                 .weight{
                    h2{
                        color: white;
                        font-weight: 400;
                        padding-bottom: 10px;
                        padding-left: 10px;
                    }
                    .all-buttons-weight{
                        .weight-item{
                            margin: 0 10px;
                            input{
                                display: none;
                            }
                            label{
                                display: inline-block;
                                padding: 20px;
                                img{
                                    width: 70px;
                                   filter: brightness(0)  grayscale(100%);
                                    
                                }
                            }
                        }
                    }

                }
            }

        }

        .expand{
            display: flex;
            align-items: center;
            justify-content: center;
            

            .btn-container{
                background-color: #616161;
                width:250px;
                display: flex;
                align-items: center;
                justify-content: center;

                button{
                    font-size: 18px;
                    text-transform: uppercase;
                    background-color: transparent;
                    border:none;
                    color: white;
                    padding: 20px;
                    text-decoration: underline;
                }
            }
        }
       
    }


}

</style>