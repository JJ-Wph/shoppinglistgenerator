<template>
  <HeaderBar/>
</template>

<script>
import HeaderBar from './components/HeaderBar.vue';
export default {
  name: 'App',
  components: {
    HeaderBar
  },
  setup(){
    return {
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald&display=swap');
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100vh;
}
#app {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-template-rows: repeat(6, 1fr);
  grid-column-gap: 0px;
  grid-row-gap: 0px;
  font-family: 'Oswald', sans-serif;
  width: 100%;
  height: 100vh;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(21, 113, 24);
}
</style>