<template>
  <div id="app">
    <header>
      <h1>Cats</h1>
    </header>
    <router-view/>
  </div>
</template>

<style lang="scss">
  html,
  body {
    width: 100%;
    height: 100%;
    padding: 0;
    margin: 0;
    * {
      padding: 0;
      margin: 0;
    }
    ::-webkit-scrollbar {
      width: 0;
    }
  }
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    header {
      background: linear-gradient(45deg, #5e02ff, #07b8ff);
      h1 {
        text-align: left;
        margin: 0;
        padding: 0.6rem 1rem;
        color: white;
      }
    }
  }
</style>
