<template>
  <div class="container">
    <div class="recipeDiv" :class="{vegeBackground: recipe.vegan}" v-for="recipe in breakfastRecipes" v-bind:key="recipe.firstName">
      <img src="../assets/vege-icon.svg" v-if="recipe.vegan" class="vegeIcon" alt="vege">
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
  align-items: center;
  background: rgb(0, 0, 0);
}

.recipeDiv {
  display: flex;
  position: relative;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  margin: 2vh;
  width: 20vw;
  height: 50vh;
  border-radius: 15px;
  background: rgb(238,8,8);
  background: linear-gradient(202deg, rgba(158,153,153,0.7987570028011204) 0%, rgba(79,65,65,0.8015581232492998) 28%, rgba(43,25,24,0.7987570028011204) 61%, rgba(136,102,93,0.804359243697479) 92%);
}

.vegeIcon {
  display: block;
  position: absolute;
  float: left;
  left: 80%;
  bottom: 85%;
  width: 30px;
  filter: invert(43%) sepia(78%) saturate(2694%) hue-rotate(78deg) brightness(90%) contrast(94%);
}

.vegeBackground {
  background: linear-gradient(to bottom left, rgba(19, 155, 17, 0.753), rgb(79,65,65,0.8015581232492998), rgb(79,65,65,0.8015581232492998), rgb(79,65,65,0.8015581232492998));
}

</style>