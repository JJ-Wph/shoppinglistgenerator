<template>
    <div class="container">
        <div class="recipeDiv" v-for="recipe in snackRecipes" v-bind:key="recipe.id">
            <p> {{ recipe.firstName }} </p>
            <button @click="recipe.addMethod">Dodaj do listy</button>
            <button @click="recipe.deleteMethod">Usuń z listy</button>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'SnackComponent',
    setup(props, {emit}){
        const snackRecipes = ref([
            {        
                firstName: 'Chipsy solone',
                typeOfMeal: 'przekąska',
                vegan: false,
                addMethod: addChips,
                deleteMethod: deleteChips
            },
            {
                firstName: 'Chipsy marchewkowe',
                typeOfMeal: 'przekąska',
                vegan: true,
                addMethod: addCarrotChips,
                deleteMethod: deleteCarrotChips
            },
            {
                firstName: 'Czekolada',
                typeOfMeal: 'przekąska',
                vegan: false,
                addMethod: addChocolate,
                deleteMethod: deleteChocolate
            },
            {
                firstName: 'Paluszki',
                typeOfMeal: 'przekąska',
                vegan: true,
                addMethod: addSticks,
                deleteMethod: deleteSticks
            },
        ])

        function addChips() {
            emit('addChipsToList', snackRecipes.value[0]);
        }

        function addCarrotChips(){
            emit('addCarrotChipsToList', snackRecipes.value[1]);
        }

        function addChocolate() {
            emit('addChocolateToList', snackRecipes.value[2]);
        }

        function addSticks() {
            emit('addSticksToList', snackRecipes.value[3]);
        }

        function deleteChips() {
            emit('deleteChipsFromList', snackRecipes.value[0]);
        }

        function deleteCarrotChips() {
            emit('deleteCarrotChipsFromList', snackRecipes.value[1]);
        }
        
        function deleteChocolate() {
            emit('deleteChocolateFromList', snackRecipes.value[2]);
        }

        function deleteSticks() {
            emit('deleteSticksFromList', snackRecipes.value[3]);
        }

    return { 
        snackRecipes,
        addChocolate,
        addCarrotChips, 
        addSticks, 
        addChips,
        deleteChips,
        deleteCarrotChips,
        deleteChocolate,
        deleteSticks

      }
    }
}
</script>

<style>

</style>