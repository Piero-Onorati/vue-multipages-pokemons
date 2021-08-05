<template>
    <div class="card">
        <div class="img-card">
            <img :src="pokemon.image" :alt="pokemon.name">
        </div>
        <h5>N &deg; {{pokemon.id}}</h5>
        <h3>{{pokemon.name}}</h3>
        <ul >
            <li v-for="(type,index) in pokemon.type" :key="index" :class="type">{{type}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name:'PokeCard',
    props:{
        pokemon:Object
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

}

</style>