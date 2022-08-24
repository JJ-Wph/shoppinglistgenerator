<template>
      <div class="container">
    <div class="recipeDiv" v-for="recipe in lunchRecipes" v-bind:key="recipe.firstName">
      <p> Posiłek {{ recipe.vegan }} </p>
      <p> {{ recipe.firstName }} </p>
      <p> {{ recipe.typeOfMeal }} </p>
      <button @click="recipe.addMethod">Dodaj do listy</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
    name: 'LunchComponent',
    setup() {
        const lunchRecipes = ref([
            {
                firstName: 'Makaron z kurczakiem',
                typeOfMeal: 'obiad',
                vegan: false,
                addMethod: addChickenPasta,
                onion: 20,
                tomato: 200,
                pasta: 200,
                chicken: 100,
                cheese: 30,
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
        ]);

        function addChickenPasta(){
            console.log(lunchRecipes.value[2].sweetPotato);
        }

        function addCheeseburger(){
            console.log('234t5r');
        }

        function addPancakes(){
            console.log('45trf');
        }

        function addVegeNuggets(){
            console.log('45trf');
        }

        return {
            lunchRecipes,
            addChickenPasta,
            addCheeseburger,
            addPancakes,
            addVegeNuggets
        }


    }
}
</script>

<style>

</style>