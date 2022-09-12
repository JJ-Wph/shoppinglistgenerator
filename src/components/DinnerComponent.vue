<template>
    <div class="container">
        <div class="recipeDiv" :class="{vegeBackground: recipe.vegan, countBackground: recipe.count > 0, countVegeBackground: recipe.vegan && recipe.count > 0}" v-for="recipe in dinnerRecipes" v-bind:key="recipe.firstName">
            <img src="../assets/vege-icon.svg" v-if="recipe.vegan" class="vegeIcon" alt="vege">
            <p> {{ recipe.firstName }} </p>
            <img class="recipeImg" :src="require('../assets/' + recipe.image + '.png')" alt="">
            <p class="countNumber" v-if="recipe.count > 0"> {{ recipe.count }} </p>
            <div class="buttonContainer">
                <button @click="recipe.addMethod">Dodaj do listy</button>
                <button @click="recipe.deleteMethod">Usuń z listy</button>
            </div>
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
                deleteMethod: deleteChickenSalad,
                image: 'chickensalad',
                count: 0,
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
                deleteMethod: deleteCheeseSandwich,
                image: 'cheesesandwich',
                count: 0,
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
                deleteMethod: deleteTofuSalad,
                image: 'tofusalad',
                count: 0,
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
                deleteMethod: deleteSweetPotatos,
                image: 'sweetpotato',
                count: 0,
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

        function deleteChickenSalad(){
            emit('deleteChickenSaladFromList', dinnerRecipes.value[0]);
        }

        function deleteCheeseSandwich(){
            emit('deleteCheeseSandwichFromList', dinnerRecipes.value[1]);
        }

        function deleteTofuSalad(){
            emit('deleteTofuSaladFromList', dinnerRecipes.value[2]);
        }

        function deleteSweetPotatos(){
            emit('deleteSweetPotatosFromList', dinnerRecipes.value[3]);
        }
 

        return{
            dinnerRecipes,
            addChickenSalad,
            addCheeseSandwich,
            addSweetPotatos,
            addTofuSalad,
            deleteChickenSalad,
            deleteCheeseSandwich,
            deleteTofuSalad,
            deleteSweetPotatos
        }
    }
}
</script>

<style>

</style>