<template>
    <section>

        <!-- start CARD -->
        <div class="card">

            <!--  start IMG CARD BOx: contains IMAGE + BUTTON for MODAL CARD -->
            <div class="img-card">

                <!-- IMG -->
                <img :src="pokemon.image" :alt="pokemon.name">

                <!-- BUTTON for MODAL CARD -->
                <button class="show" @click="show=true">
                    <img src="../assets/img/icons8-pokeball-100-1.png" alt="">
                </button>

            </div>
            <!-- end IMG CARD BOx -->

            <!-- Pokémon NUMBER -->
            <h5>N &deg; {{pokemon.id}}</h5>

            <!-- Pokémon NAME -->
            <h3>{{pokemon.name}}</h3>

            <!-- Pokémon TYPE -->
            <ul >
                <li v-for="(type,index) in pokemon.type" :key="index" :class="type">{{type}}</li>
            </ul>


            <!-- start MODAL CARD: IMAGE + TEXT -->
            <div class="modal-card" v-if="show">

                <!-- MODAL CARD: IMAGE -->
                <div class="modal-card-img">
                    <img :src="pokemon.img" :alt="pokemon.name">
                </div>

                <!-- MODAL CARD: TEXT -->
                <div class="modal-card-text">

                    <!-- Pokemon-description -->
                    <div class="pokemon-description">
                        <div class="number_name">
                            <!-- Pokemon Number -->
                            <span class="num">N &deg; {{pokemon.id}}</span>
                            <!-- Pokemon Nsme -->
                            <h2>{{pokemon.name}}</h2>
                        </div>

                        <!-- 'close the modal' button -->
                        <button  @click="show=false">close</button>
                    </div>

                    <!-- Pokemon type -->
                    <div class="pokemon-type">
                        <ul>
                            <li v-for="(type,index) in pokemon.type" :key="index" :class="type">{{type}}</li>
                        </ul>
                    </div>

                    <!-- Details: height, weight, abilities and moves -->
                    <div class="details">
                        <!-- Height -->
                        <h4>Altezza: <span class="numbers" id="height">{{pokemon.height}} dm</span></h4>
                        <!-- Weight -->
                        <h4>Peso: <span class="numbers">{{pokemon.weight}} hg</span></h4>
                        <!-- Abilities -->
                        <h4>Abilities:
                            <span class="ability" v-for="(ability,index) in pokemon.abilities" :key="'j'+ index" :class="type">{{ability}}</span>
                        </h4>
                        <!-- Moves -->
                        <h4>Move: <span class="move">{{pokemon.move}}</span></h4>
                    </div>

                    <!-- Table with all values of attack, defence, etc -->
                    <table>
                        <tr>
                            <th v-for="(x,index) in pokemon.stats" :key="'k'+ index">{{x}}</th>
                        </tr>
                        <tr>
                            <td v-for="(y,index) in pokemon.stats_number" :key="'l'+ index">{{y}}</td>

                        </tr>
                    </table>

                </div>

            </div>
            <!-- end MODAL CARD -->

        </div>
        <!-- end CARD -->

        <div class="background" v-if="show"></div>

    </section>
</template>

<script>
export default {
    name:'PokeCard',
    props:{
        pokemon:Object
    },
    data(){
        return{
            show:false
        }
    }

}
</script>

<style lang="scss" scoped>

.card{
    background-color: #fff;
    .img-card{
        background-color: #f2f2f2;
        border-radius: 5px ;
        text-align: center;
        position: relative;

        img{
            width:60%
        }
    }

    h5{
        padding-top: 3px;
        color: #3e3e3e;
    }

    h3{
        color: #282828;
        padding: 8px 0 4px 0;
    }

    ul{
        display:flex;

        li{
            font-size: 12px;
            padding: 2px 0;
            width:70px;
            text-align: center;
            list-style: none;
            border-radius: 5px;
            margin-right:10px;
        }
    }

    &:hover{
        animation: bounce 0.5s linear;
    }

    &:hover button.show{
        display: block;
    }

    button.show{
        background-color: transparent;
        border: none;
        display: none;
        position: absolute;
        filter: invert(0.6);
        top:50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index:4;
        img{
            width:40px
        }

    }

    .modal-card{
        background-color: white;
        padding: 10px;
        border-radius:5px;
        width: 940px;
        position: fixed;
        z-index:500;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        display: flex;
        align-items: center;
        background-image: url('../assets/img/new-pokemon.png');
        background-size: 70%;
        background-repeat: no-repeat;
        background-position: center right;
        box-shadow: 0 1px 3px rgba(0,0,0, 0.12), 0 1px 2px rgba(0,0,0, 0.24) ;
         

        .modal-card-img{
            width: 450px;
            height: 450px;
            border-radius:5px;
            background-color: #f2f2f2;
            img{
                width:100%
            }
        }

        .modal-card-text{
            padding: 5px 5px 5px 15px;
            border-radius: 5px ;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            

            .pokemon-description{
                color:#282828;
                display: flex;
                justify-content: space-between;
                align-items: flex-start;

                .number_name{

                    .num{
                        font-weight: 500;
                        color: #3e3e3e;
                    }
                }

                button{
                    background-color: #e3350d;
                    color:white;
                    font-size: 16px;
                    padding: 5px 10px;
                    cursor: pointer;

                    &:hover{
                        background-color: #b32e10;
                    }

                }
            }

            .pokemon-type{
                margin-bottom: 30px;
            }

            .details{
                margin: 50px 0 20px 0;
                background-color:#cfd8dc88;
                color:#3e3e3e;
                border-radius: 5px ;
                padding: 5px;
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                justify-content: space-between;

                span.numbers{
                    color:#545b62
                }

                span.ability{
                    background-color: #90a4ae;
                    color: white;
                    padding:3px 10px;
                    font-weight:400;
                    font-size: 12px;
                    text-transform: uppercase;
                    border-radius:5px ;
                    margin:0 5px ;
                }

                span.move{
                    background-color: #e6bc2f;
                    color: white;
                    padding:3px 10px;
                    font-weight:400;
                    font-size: 12px;
                    text-transform: uppercase;
                    border-radius:5px ;
                    margin:0 5px ;

                }

                h4{
                    margin: 5px 0;
                }
            }

            table{
                margin: 10px 0;
                th{
                    background-color: #30a7d7;
                    color:whitesmoke;
                    font-size: 15px;
                }

                td{
                    text-align: center;
                    background-color: whitesmoke;
                }

                td, th {
                border: 1px solid #ddd;
                padding: 5px;
                width: calc(100% / 6);

                }
            }
        }

    }

}

.background{
    position: fixed;
    top:0;
    left:0;
    width: 100vw;
    height: 100vh;
    transition: 200ms ease-in-out;
    background-color: rgba(0,0,0, 0.5);
    z-index: 45;
}

</style>