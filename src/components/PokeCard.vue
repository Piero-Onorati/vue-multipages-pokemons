<template>
  <div>
        <h2>{{pokemon.name}}</h2>
        <h3>{{pokemon.id}}</h3>
        <img :src="pokemon.image" alt="">
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

<style>

</style>