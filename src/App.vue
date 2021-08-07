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
</style>
