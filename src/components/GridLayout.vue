<template>
<section>
    <div class="btn-pokedex-div">
        <button class="btn-pokedex"><router-link :to="{name: 'Pokedex'}"><span>See all the Pokémons</span></router-link></button>
    </div>
    <div class="grid-container">
        <div class="item1"><img src="../assets/img/wp4565982-pokemon-sword-and-shield-desktop-wallpapers.jpg" alt=""></div>
        <div class="item2"><img src="../assets/img/wp4433400-pokemon-the-series-sun-and-moon-ultra-legends-wallpapers.jpg" alt=""></div>
        <div class="item3"><img src="../assets/img/pokemon-movie.jpg" alt=""></div>  
    </div>
</section>
</template>

<script>
export default {

}
</script>

<style>

.btn-pokedex-div{
    background-color: white;
    display: flex;
    justify-content: center;
    padding: 10px 0;
}

.btn-pokedex{
    background-color: #525252;
    border:2px solid #525252;
}

.btn-pokedex>a{
    display: inline-block;
    color:white;
    text-decoration: none;
    font-weight: 500;
    font-size: 18px;
    padding: 10px 20px;
}

.item1 { grid-area: header; }
.item2 { grid-area: menu; }
.item3 { grid-area: main; }


.grid-container {
  display: grid;
  grid-template-areas:
    'menu menu menu header header header'
    'menu menu menu header header header'
    'menu menu menu main main main '
    'menu menu menu main main main ';
  grid-gap: 50px;
  background-color: white;
  padding: 30px 10px;
  margin-bottom: 50px;
}

.grid-container > div {
  text-align: center;
  font-size: 30px;
}

.item1 img, .item2 img, .item3 img{
    width:100%
}


</style>