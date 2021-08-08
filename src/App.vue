<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">
        <div class="nav-item">
          <img src="@/assets/img/icons8-pokemon.gif" alt="pikachu-gif">
          <span>Home</span> 
        </div>
      </router-link>
      <router-link :to="{name: 'Pokedex'}">
        <div class="nav-item">
          <img src="@/assets/img/icons8-pokedex-100.png" alt="pokedex-icon">
          <span>Pokédex</span> 
        </div>
      </router-link>
      <router-link :to="{name: 'GCCPokemon'}">
        <div class="nav-item">
          <img src="@/assets/img/icons8-stella-pokemon-100.png" alt="star-icon">
          <span>GCCPokemon</span> 
        </div>
      </router-link>
    </div>
    <router-view/>

    <footer>

      <div class="social-icons">
        <h4>Follow Pokémon on social</h4>
        <div class="icons">
          <img src="@/assets/img/social/email-icon.jpg" alt="email icon">
          <img src="@/assets/img/social/instagram-icon.jpg" alt="instagram icon">
          <img src="@/assets/img/social/twitch-icon.jpg" alt="twich icon">
          <img src="@/assets/img/social/twitter-icon.jpg" alt="twitter icon">
        </div>
      </div>

    </footer>
  </div>
</template>


<style lang="scss">
@import '@/style/commons.scss';



#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#nav {
  display:flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  width:100%;
  position: fixed;
  z-index: 10;
  top:0%;
  left:0%;
  padding-top: 15px;


  a {
    font-weight: bold;
    padding: 0 10px 10px 10px;
    color: #2c3e50;
    display:inline-block;
    text-decoration: none;
    
    &.router-link-exact-active {
      color: #42b983;
      border-bottom: 4px solid #42b983;

    }
  }

  .nav-item{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 20px;

    img{
      width: 30px;
      margin-bottom: 5px;
    }
  }

  
}

footer{
  background-color: #1f1f1f;
  display: flex;
  align-items:center ;
  justify-content: center;
  padding: 50px 0;

  .social-icons{
    display: flex;
    align-items: center;
    flex-direction: column;

    h4{
      color: white;
      padding-bottom: 20px;
    }

    img{
      width:50px;
      filter: grayscale(100%);
      margin: 0 10px;
      cursor: pointer;

      &:hover{
        filter: grayscale(0%);

      }
    }
  }

}
</style>
