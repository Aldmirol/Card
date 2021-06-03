<template>
  <div id="app">
    <Card />
  </div>
</template>

<script>
import Card from './components/Card';

export default {
  name: 'App',
  components: {
    Card
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700;900&display=swap');

  #app {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #E1E1E1;
    font-family: 'Roboto', sans-serif;
    color: #2C363D;
  }
</style>
