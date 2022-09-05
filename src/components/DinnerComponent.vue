<template>
    <div class="container">
        <div class="recipeDiv" v-for="recipe in dinnerRecipes" v-bind:key="recipe.firstName">
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
    name: 'DinnerComponent',
    setup(props, {emit}) {
        const dinnerRecipes = ref([
            {
                firstName: 'Sałatka z kurczakiem',
                typeOfMeal: 'kolacja',
                vegan: false,
                addMethod: addChickenSalad,
                chicken: 150,
                chickPeas: 100,
                tomato: 150,
                cucumber: 100,
                chives: 50,
                mayonnaise: 50,
            },
            {
                firstName: 'Kanapki z serem żółtym',
                typeOfMeal: 'kolacja',
                vegan: false,
                addMethod: addCheeseSandwich,
                cheese: 100,
                roll: 1,
                tomato: 50,
                cucumber: 50,
            },
            {
                firstName: 'Sałatka z tofu',
                typeOfMeal: 'kolacja',
                vegan: true,
                addMethod: addTofuSalad,
                tofu: 150,
                chickPeas: 100,
                tomato: 150,
                cucumber: 100,
                chives: 50,
                mayonnaise: 50,
            },
            {
                firstName: 'Pieczone bataty z pomidorami',
                typeOfMeal: 'kolacja',
                vegan: true,
                addMethod: addSweetPotatos,
                sweetPotato: 300,
                tomato: 200,
            },
        ]);

        function addChickenSalad(){
            emit('addChickenSaladToList', dinnerRecipes.value[0]);
        }

        function addCheeseSandwich(){
            emit('addCheeseSandwichToList', dinnerRecipes.value[1]);
        }

        function addTofuSalad(){
            emit('addTofuSaladToList', dinnerRecipes.value[2]);
        }
        function addSweetPotatos(){
            emit('addSweetPotatosToList', dinnerRecipes.value[3]);
        }

        return{
            dinnerRecipes,
            addChickenSalad,
            addCheeseSandwich,
            addSweetPotatos,
            addTofuSalad,
        }
    }
}
</script>

<style>

</style>