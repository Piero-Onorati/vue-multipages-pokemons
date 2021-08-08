<template>
    <section>
        <div class="card">
            <div class="img-card">
                <img :src="pokemon.image" :alt="pokemon.name">
                <button class="show" @click="show=true">
                    <img src="../assets/img/icons8-pokeball-100-1.png" alt="">
                </button>
            </div>
            <h5>N &deg; {{pokemon.id}}</h5>
            <h3>{{pokemon.name}}</h3>
            <ul >
                <li v-for="(type,index) in pokemon.type" :key="index" :class="type">{{type}}</li>
            </ul>
            <div class="description" v-if="show">
                <div class="img-description">
                    <img :src="pokemon.img" :alt="pokemon.name">
                </div>
                <div class="text-description">
                    <div class="name_type">
                        <button  @click="show=false">close</button>
                        <div class="pokemon-name">
                            <span>N &deg; {{pokemon.id}}</span>
                            <h2>{{pokemon.name}}</h2> 
                        </div>
                        <div class="pokemon-type">
                            <ul>
                                <li v-for="(type,index) in pokemon.type" :key="index" :class="type">{{type}}</li>
                            </ul>
                        </div>
                    </div>
                    <div class="details">
                        <h4>Altezza: {{pokemon.height}} dm</h4>
                        <h4>Peso: {{pokemon.weight}} hg</h4>
                        <h4>Abilities: 
                            <span class="ability" v-for="(ability,index) in pokemon.abilities" :key="'j'+ index" :class="type">{{ability}}</span>
                        </h4>
                        <h4>Move: {{pokemon.move}}</h4>
                    </div>

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
        </div>
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
    cursor: pointer;
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
        img{
            width:40px
        }

    }

    .description{
        background-color: white;
        padding: 10px;
        border-radius:5px;
        width: 900px;
        position: fixed;
        z-index:12;
        top:50%;
        left: 50%;
        transform: translate(-50%,-50%);
        display: flex;
        align-items: center;

        .img-description{
            width: 400px;
            height: 400px;
            border-radius:5px;
            background-color: #f2f2f2;
            img{
                width:100%
            }
        }

        .text-description{
            padding: 5px 15px;
            border-radius: 5px ;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            

            .details{
                margin: 10px 0; 
                background-color:#a4a4a4 ;
                border-radius: 5px ; 
                padding: 5px;
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                justify-content: space-between;

                span.ability{
                    background-color: rgba(0, 0, 0, 0.377);
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
    bottom:0;
    right: 0;
    transition: 200ms ease-in-out;
    background-color: rgba(0,0,0, 0.5);
    pointer-events: none;
    z-index: 11;
}

</style>