<template>
    <div class="container">
        <div class="recipeDiv" v-for="recipe in snackRecipes" v-bind:key="recipe.id">
            <p> Posiłek {{ recipe.id }} </p>
            <p> {{ recipe.firstName }} </p>
            <p> {{ recipe.typeOfMeal }} </p>
            <button @click="recipe.addMethod">Dodaj do listy</button>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'SnackComponent',
    setup(){
        const snackRecipes = ref([
            {        
                firstName: 'Chipsy solone',
                typeOfMeal: 'przekąska',
                vegan: false,
                addMethod: addChips,
            },
            {
                firstName: 'Chipsy marchewkowe',
                typeOfMeal: 'przekąska',
                vegan: true,
                addMethod: addCarrotChips,
            },
            {
                firstName: 'Czekolada',
                typeOfMeal: 'przekąska',
                vegan: false,
                addMethod: addChocolate,
            },
            {
                firstName: 'Paluszki',
                typeOfMeal: 'przekąska',
                vegan: true,
                addMethod: addSticks,
            },
        ])

        function addChocolate() {
        console.log('q3rwe');
        }

        function addCarrotChips(){
        console.log('32rwefd');
        }

        function addSticks() {
        console.log('dp');
        }

        function addChips() {
        console.log('dpe');
        }

    return { 
        snackRecipes,
        addChocolate,
        addCarrotChips, 
        addSticks, 
        addChips, 
      }
    }
}
</script>

<style>

</style>