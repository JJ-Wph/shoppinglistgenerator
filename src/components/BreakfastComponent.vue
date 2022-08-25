<template>
  <div class="container">
    <div class="recipeDiv" v-for="recipe in breakfastRecipes" v-bind:key="recipe.id">
      <p> Posiłek {{ recipe.id }} </p>
      <p> {{ recipe.firstName }} </p>
      <p> {{ recipe.typeOfMeal }} </p>
      <button @click="recipe.addMethod">Dodaj do listy</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: 'BreakfastComponent',
  setup() {
    const breakfastRecipes = ref([
      {
        firstName: 'Jajecznica na boczku z pomidorami',
        typeOfMeal: 'śniadanie',
        vegan: false,
        addMethod: addScrambledEggs,
        eggs: 4,
        onion: 40,
        bacon: 100,
        roll: 2,
        tomato: 200,
      },
      {
        firstName: 'Placki skyrowe',
        typeOfMeal: 'śniadanie',
        vegan: false,
        addMethod: addSkyrPancakes,
        eggs: 1,
        vanillaSkyr: 150,
        flour: 40,
      },
      {
        firstName: 'Pasta jajeczna',
        typeOfMeal: 'śniadanie',
        vegan: false,
        addMethod: addEggSalad,
        eggs: 2,
        mayonnaise: 50,
        roll: 1,
        chives: 50,
      },
      {
        firstName: 'Pasta z tofu',
        typeOfMeal: 'śniadanie',
        vegan: true,
        addMethod: addTofuPaste,
        tofu: 200,
        roll: 1,
        tomato: 50,      
      },
      

      ]);


    function addScrambledEggs(){
      console.log(breakfastRecipes.value[0].eggs);
    }

    function addSkyrPancakes(){
      console.log(breakfastRecipes.value[2].mayonnaise);
    }

    function addEggSalad(){
      console.log(breakfastRecipes.value[1].firstName);
    }

    function addTofuPaste(){
      console.log(breakfastRecipes.value[2].chives);
    }

 





    return { 
      breakfastRecipes,  
      addScrambledEggs, 
      addTofuPaste,
      addSkyrPancakes,
      addEggSalad,
      }
  }
};
</script>


<style>

.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: auto;
  height: auto;
  padding: 0;
  margin: 0;

}

.recipeDiv {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  margin: 2vh;
  width: 20vw;
  height: 30vh;
  border: 1px solid green;

}


</style>