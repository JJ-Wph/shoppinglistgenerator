<template>
  <div class="recipeDiv" v-for="recipe in recipes" v-bind:key="recipe.id">
    <p> Posiłek {{ recipe.id }} </p>
    <p> {{ recipe.firstName }} </p>
    <p> {{ recipe.typeOfMeal }} </p>
    <button @click="recipe.addMethod">Dodaj do listy</button>
  </div>
  <div class="recipeDiv">
    <p>{{listOfIgredients.bacon}}</p>
    <p>{{listOfIgredients.eggs}}</p>
    <p>{{listOfIgredients.roll}}</p>
  </div>
</template>

<script>
import { ref, reactive } from "vue";

export default {
  name: "MyComponent",
  setup() {
    const recipes = ref([
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
        firstName: 'Cheeseburger',
        typeOfMeal: 'obiad',
        vegan: false,
        addMethod: addCheeseburger,
        onion: 20,
        tomato: 100,
        roll: 1,
        bacon: 100,
        beef: 100,
        cheese: 30,
      },
      {
        firstName: 'Naleśniki z serem',
        typeOfMeal: 'obiad',
        vegan: false,
        addMethod: addPancakes,
        flour: 130,
        eggs: 1,
        milk: 250,
        curds: 100,
        raisins: 15,
      },
      {
        firstName: 'Wege Nuggetsy',
        typeOfMeal: 'obiad',
        vegan: true,
        addMethod: addVegeNuggets,
        sweetPotato: 500,
        chickPeas: 240,
        breadCrumbs: 100,
        sweetPepper: 2,
      },
      {

      }
      
      
      
      
      ]);
    





    const listOfIgredients = reactive({
      onion: 0,
      tomato: 0,
      roll: 0,
      bacon: 0,
      cheese: 0,
      eggs: 0,
      beef: 0,
      flour: 0,
      milk: 0,
      curds: 0,
      raisins: 0,
    });


    function addScrambledEggs(){
      console.log(recipes.value[0].eggs);
    }

    function addCheeseburger() {
      console.log('recipeburger');
    }

    function addPancakes(){
      console.log('dupa pipa');
    }

    function addVegeNuggets(){
      console.log(recipes.value[3].sweetPotato);
    }



    return { recipes, listOfIgredients, addScrambledEggs, addCheeseburger, addPancakes, addVegeNuggets }
  }
};
</script>


<style>
.recipeDiv {
  display: flex;
  flex-wrap: wrap-reverse;
  flex-direction: column;
  justify-items: center;
  align-items: center;
  width: 30%;
  height: 80%;
  border: 1px solid green;
  margin: auto;
  padding: auto;
  vertical-align: bottom;
}


</style>