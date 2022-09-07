<template>
    <div class="container">
        <div class="recipeDiv" v-for="recipe in lunchRecipes" v-bind:key="recipe.firstName">
            <p v-if="recipe.vegan">Posiłek &#127807;</p>
            <p> {{ recipe.firstName }} </p>
            <p> {{ recipe.typeOfMeal }} </p>
            <button @click="recipe.addMethod">Dodaj do listy</button>
            <button @click="recipe.deleteMethod"></button>
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
export default {
    name: 'LunchComponent',
    setup(props, {emit}) {
        const lunchRecipes = ref([
            {
                firstName: 'Makaron z kurczakiem',
                typeOfMeal: 'obiad',
                vegan: false,
                addMethod: addChickenPasta,
                deleteMethod: deleteChickenPasta,
                count: 0,
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
                deleteMethod: deleteCheeseburger,
                count: 0,
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
                deleteMethod: deletePancakes,
                count: 0,
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
                deleteMethod: deleteVegeNuggets,
                count: 0,
                sweetPotato: 500,
                chickPeas: 240,
                breadCrumbs: 100,
                sweetPepper: 2,
            },
        ]);

        function addChickenPasta(){
            emit('addChickenPastaToList', lunchRecipes.value[0]);
        }

        function addCheeseburger(){
            emit('addCheeseburgerToList', lunchRecipes.value[1]);
        }

        function addPancakes(){
            emit('addPancakesToList', lunchRecipes.value[2]);
        }

        function addVegeNuggets(){
            emit('addVegeNuggetsToList', lunchRecipes.value[3]);
        }

        function deleteChickenPasta(){
            emit('deleteChickenPastaFromList', lunchRecipes.value[0]);
        }

        function deleteCheeseburger(){
            emit('deleteCheeseburgerFromList', lunchRecipes.value[1]);
        }

        function deletePancakes(){
            emit('deletePancakesFromList', lunchRecipes.value[2]);
        }

        function deleteVegeNuggets(){
            emit('deleteVegeNuggetsFromList', lunchRecipes.value[3]);
        }

        return {
            lunchRecipes,
            addChickenPasta,
            addCheeseburger,
            addPancakes,
            addVegeNuggets,
            deleteChickenPasta,
            deleteCheeseburger,
            deletePancakes,
            deleteVegeNuggets
        }


    }
}
</script>

<style>

</style>