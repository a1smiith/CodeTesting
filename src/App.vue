<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Press Start 2P', 'VT323';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000;
  font-weight: bold;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
