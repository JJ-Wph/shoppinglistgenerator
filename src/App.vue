<template>
  <HeaderBar/>
  <BreakfastComponent v-if="isBreakfastActive"/>
  <LunchComponent v-if="isLunchActive"/>
  <DinnerComponent v-if="isDinnerActive"/>
  <SnackComponent v-if="isSnackActive"/>
</template>

<script>
import HeaderBar from './components/HeaderBar.vue';
import BreakfastComponent from './components/BreakfastComponent.vue'
import LunchComponent from './components/LunchComponent.vue'
import DinnerComponent from './components/DinnerComponent.vue'
import SnackComponent from './components/SnackComponent.vue';

import {ref} from 'vue';
export default {
  name: 'App',
  components: {
    HeaderBar,
    BreakfastComponent,
    LunchComponent,
    DinnerComponent,
    SnackComponent
  },

  setup(){
    const isBreakfastActive = ref(true);
    const isLunchActive = ref(false);
    const isDinnerActive = ref(false);
    const isSnackActive = ref(false);

    return {
      isBreakfastActive, 
      isLunchActive, 
      isDinnerActive, 
      isSnackActive
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
