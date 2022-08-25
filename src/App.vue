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
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans:wght@300&display=swap');

body {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
}

#app {
  display: flex;
  flex-direction: column;
  font-family: 'Noto Sans', sans-serif;
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: lightblue;
  text-align: center;
  background-color: darkgrey;
};



</style>
