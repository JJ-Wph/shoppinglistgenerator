<template>
  <div class="container">
    <div class="recipeDiv" v-for="recipe in breakfastRecipes" v-bind:key="recipe.id">
      <p v-if="recipe.vegan">Posiłek &#127807;</p>
      <p> {{ recipe.firstName }} </p>
      <p> {{ recipe.typeOfMeal }} </p>
      <p v-if="recipe.count > 0"> {{ recipe.count }} </p>
      <button @click="recipe.addMethod">Dodaj do listy</button>
      <button @click="recipe.deleteMethod">Usuń z listy</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: 'BreakfastComponent',
  setup(props, {emit}) {
    const breakfastRecipes = ref([
      {
        firstName: 'Jajecznica na boczku z pomidorami',
        typeOfMeal: 'śniadanie',
        vegan: false,
        addMethod: addScrambledEggs,
        deleteMethod: deleteScrambledEggs,
        count: 0,
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
        deleteMethod: deleteSkyrPancakes,
        count: 0,
        eggs: 1,
        vanillaSkyr: 150,
        flour: 40,
      },
      {
        firstName: 'Pasta jajeczna',
        typeOfMeal: 'śniadanie',
        vegan: false,
        addMethod: addEggSalad,
        deleteMethod: deleteEggSalad,
        count: 0,
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
        deleteMethod: deleteTofuPaste,
        count: 0,
        tofu: 200,
        roll: 1,
        tomato: 50,      
      },
      

      ]);


    function addScrambledEggs(){
      emit('addEggsToList', breakfastRecipes.value[0]);
    }

    function addSkyrPancakes(){
      emit('addSkyrPancakesToList', breakfastRecipes.value[1]);
    }

    function addEggSalad(){
      emit('addEggSaladToList', breakfastRecipes.value[2]);
    }

    function addTofuPaste(){
      emit('addTofuPasteToList', breakfastRecipes.value[3]);
    }

    function deleteScrambledEggs() {
      emit('deleteScrambledEggsFromList', breakfastRecipes.value[0]);
    }

    function deleteSkyrPancakes() {
      emit('deleteSkyrPancakesFromList', breakfastRecipes.value[1]);
    }

    function deleteEggSalad() {
      emit('deleteEggSaladFromList', breakfastRecipes.value[2]);
    }

    function deleteTofuPaste() {
      emit('deleteTofuPasteFromList', breakfastRecipes.value[3]);
    }
 





    return { 
      breakfastRecipes,  
      addScrambledEggs, 
      addTofuPaste,
      addSkyrPancakes,
      addEggSalad,
      deleteScrambledEggs,
      deleteSkyrPancakes,
      deleteEggSalad,
      deleteTofuPaste
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
  background: linear-gradient(to top right, red, rgb(63, 63, 63), rgb(63, 63, 63), rgb(63, 63, 63));
}


</style>