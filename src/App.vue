<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>
      <router-link :to="{name: 'Pokedex'}">Pokédex</router-link>
      <router-link :to="{name: 'GCCPokemon'}">GCCPokemon</router-link>
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
   text-align: center;
  background-color: white;
  width:100%;
  position: fixed;
  top:0%;
  left:0%;
  padding: 20px 0;

  a {
    font-weight: bold;
    padding: 0 10px;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
