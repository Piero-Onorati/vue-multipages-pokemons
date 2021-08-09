<template>
<section>
    <div class="btn-pokedex-div">
        <button class="btn-pokedex"><router-link :to="{name: 'Pokedex'}"><span>See all the Pokémons</span></router-link></button>
    </div>
    <div class="grid-container">
        <div class="item1">
            <img src="../assets/img/wp4565982-pokemon-sword-and-shield-desktop-wallpapers.jpg" alt="poster Pokemon game 'Spada e Scudo">
            <p> Nella regione di Galar troverai tanti nuovi e meravigliosi Pokémon, fra cui i Pokémon iniziali Grookey, Scorbunny e Sobble!</p>
        </div>
        <div class="item2">
            <img src="../assets/img/wp4433400-pokemon-the-series-sun-and-moon-ultra-legends-wallpapers.jpg" alt="poster Pokemon series 'Sun and Moon-ULtra Adventures">
            <h6>Pokemon Sun and Moon - Ultra Adventures</h6>
            <p>Segui Ash e Pikachu in questa nuova entusiasmante avventura nella regione di Alola! Gli episodi della stagione Sun and Moon - Ultra Adventures sono su K2 ogni giorno dalle 18:00.</p>
        </div>
        <div class="item3">
            <img src="../assets/img/pokemon-movie.jpg" alt="poster Pokemon movie 'In ognuno di noi">
            <p> Chissà se il coraggio di Ash e Pikachu basterà a mettere tutti in salvo in questa nuova avventura!
            Scoprilo nel nuovo Pokemon Movie: In ognuno di noi, ora disponibile su TV Pokémon.</p>
        </div>  
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

.item1 { 
    grid-area: header;
    border-radius:5px;
    overflow: hidden;
    background-color:  #b38aea;
    color: white;
}

.item1:hover{
    background-color: #a45eff;
    animation: bounce 0.5s linear;
}
.item2 { 
    grid-area: menu;
    border-radius:5px;
    overflow: hidden;
    background-color: #e6bc2f;
    color: white;
}

.item2>h6 { 
   padding-top:15px
}


.item2:hover{
    background-color: #e2ad00;
    animation: bounce 0.5s linear;
}


.item3 { 
    grid-area: main;
    border-radius:5px;
    overflow: hidden;
    background-color: #1b53ba;
    color: white;
}

.item3:hover{
    background-color: #0059ff;
    animation: bounce 0.5s linear;
}

.item1>p, .item2>p, .item3>p{
    padding:10px;
    font-size: 14px;
    line-height: 24px;
}

.item1 img, .item2 img, .item3 img{
    width:100%
}

.grid-container {
  display: grid;
  grid-template-areas:
    'menu menu menu header header header'
    'menu menu menu main main main'
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



</style>