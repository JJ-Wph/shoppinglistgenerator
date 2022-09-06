<template>
  <header>
    <h3>Shopping List Generator</h3>
    <nav>
        <ul>
            <li @click="activateBreakfast">Śniadania</li>
            <li @click="activateLunch">Obiady</li>
            <li @click="activateDinner">Kolacje</li>
            <li @click="activateSnack">Przekąski</li>
        </ul>
    </nav>
    <div class="recipeDiv">
        <template v-for="product in listOfIgredients" :key="product">
            <p v-if="product.value > 0">{{product.polishWord}}: {{product.value}}</p>
        </template>

           

    </div>
  </header>
    <BreakfastComponent 
        v-if="isBreakfastActive" 
        @add-eggs-to-list=addScrambledEggs
        @add-skyr-pancakes-to-list=addSkyrPancakes
        @add-Egg-Salad-To-List=addEggSalad
        @add-Tofu-Paste-To-List=addTofuPaste
    />

    <LunchComponent 
        v-if="isLunchActive"
        @add-Chicken-Pasta-To-List=addChickenPasta
        @add-Cheeseburger-To-List=addCheeseburger
        @add-Pancakes-To-List=addPancakes
        @add-Vege-Nuggets=addVegeNuggets
    />

    <DinnerComponent 
        v-if="isDinnerActive"
        @add-Chicken-Salad-To-List=addChickenSalad
        @add-Cheese-Sandwich-To-List=addCheeseSandwich
        @add-Tofu-Salad-To-List=addTofuSalad
        @add-Sweet-Potatos-To-List=addSweetPotatos
    />

    <SnackComponent 
        v-if="isSnackActive"
        @add-Chips-To-List=addChips
        @add-Carrot-Chips-To-List=addCarrotChips
        @add-Chocolate-To-List=addChocolate
        @add-Sticks-To-List=addSticks
        @delete-Chips-From-List=deleteChips
        @delete-Carrot-Chips-From-List=deleteCarrotChips
        @delete-Chocolate-From-List=deleteChocolate
        @delete-Sticks-From-List=deleteSticks
    />
</template>

<script>
import BreakfastComponent from './BreakfastComponent.vue'
import LunchComponent from './LunchComponent.vue'
import DinnerComponent from './DinnerComponent.vue'
import SnackComponent from './SnackComponent.vue'

import {reactive, ref} from 'vue'
export default {
    name: 'HeaderBar',
    components: {
    BreakfastComponent,
    LunchComponent,
    DinnerComponent,
    SnackComponent,
},
    setup(){
        const isBreakfastActive = ref(true);
        const isLunchActive = ref(false);
        const isDinnerActive = ref(false);
        const isSnackActive = ref(false);

        const listOfIgredients = reactive({
            onion:{ value: 0, polishWord: 'cebula'},
            tomato:{ value: 0, polishWord: 'pomidor'},
            roll:{ value: 0, polishWord: 'bułka'},
            bacon: { value: 0, polishWord: 'bekon'},
            cheese: { value: 0, polishWord: 'ser żółty'},
            eggs: { value: 0, polishWord: 'jaja'},
            beef: { value: 0, polishWord: 'wołowina'},
            flour: { value: 0, polishWord: 'mąka'},
            milk: { value: 0, polishWord: 'mleko'},
            curds: { value: 0, polishWord: 'serek wiejski'},
            raisins: { value: 0, polishWord: 'rodzynki'},
            vanillaSkyr: { value: 0, polishWord: 'skyr waniliowy'},
            mayonnaise: { value: 0, polishWord: 'majonez'},
            chives: { value: 0, polishWord: 'szczypiorek'},
            tofu: { value: 0, polishWord: 'tofu'},
            pasta: { value: 0, polishWord: 'makaron'},
            chicken: { value: 0, polishWord: 'pierś z kurczaka'},
            sweetPotato: { value: 0, polishWord: 'batat'},
            chickPeas: { value: 0, polishWord: 'ciecierzyca'},
            breadCrumbs: { value: 0, polishWord: 'bułka tarta'},
            sweetPepper: { value: 0, polishWord: 'papryka słodka'},
            cucumber: { value: 0, polishWord: 'ogórek'},
            chips: { value: 0, polishWord: 'chipsy'},
            carrotChips: { value: 0, polishWord: 'chipsy marchewkowe'},
            chocolate: { value: 0, polishWord: 'czekolada'},
            sticks: { value: 0, polishWord: 'paluszki'},
    });

        const addScrambledEggs = val => {
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.bacon.value += val.bacon;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
        }

        const addSkyrPancakes = val => {
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.vanillaSkyr.value += val.vanillaSkyr;
            listOfIgredients.flour.value += val.flour;
        }

        const addEggSalad = val => {
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.chives.value += val.chives;
        }

        const addTofuPaste = val => {
            listOfIgredients.tofu.value += val.tofu;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
        }

        const addChickenPasta = val => {
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.pasta.value += val.pasta;
            listOfIgredients.chicken.value += val.chicken;
            listOfIgredients.cheese.value += val.cheese;
        }

        const addCheeseburger = val => {
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.bacon.value += val.bacon;
            listOfIgredients.beef.value += val.beef;
            listOfIgredients.cheese.value += val.cheese;
        }

        const addPancakes = val => {
            listOfIgredients.flour.value += val.flour;
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.milk.value += val.milk;
            listOfIgredients.curds.value += val.curds;
            listOfIgredients.raisins.value += val.raisins;
        }

        const addVegeNuggets = val => {
            listOfIgredients.sweetPotato.value += val.sweetPotato;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.breadCrumbs.value += val.breadCrumbs;
            listOfIgredients.sweetPepper.value += val.sweetPepper;
        }

        const addChickenSalad = val => {
            listOfIgredients.chicken.value += val.chicken;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
            listOfIgredients.chives.value += val.chives;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
        }

        const addCheeseSandwich = val => {
            listOfIgredients.cheese.value += val.cheese;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
        }

        const addTofuSalad = val => {
            listOfIgredients.tofu.value += val.tofu;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
            listOfIgredients.chives.value += val.chives;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
        }

        const addSweetPotatos = val => {
            listOfIgredients.sweetPotato.value += val.sweetPotato;
            listOfIgredients.tomato.value += val.tomato;
        }

        const addChips = () => {
            listOfIgredients.chips.value++
        }

        const addCarrotChips = () => {
            listOfIgredients.carrotChips.value++
        }

        const addChocolate = () => {
            listOfIgredients.chocolate.value++
        }

        const addSticks = () => {
            listOfIgredients.sticks.value++
        }

        const deleteChips = () => {
            
            listOfIgredients.chips.value--
        }

        const deleteCarrotChips = () => {
            if(listOfIgredients.carrotChips.value > 0) {
                listOfIgredients.carrotChips.value--
        }}

        const deleteChocolate = () => {
            listOfIgredients.chocolate.value--
        }

        const deleteSticks = () => {
            listOfIgredients.sticks.value--
        }

        function activateBreakfast() {
            isBreakfastActive.value = true;
            isLunchActive.value = false;
            isDinnerActive.value = false;
            isSnackActive.value = false;
        }

        function activateLunch() {
            isBreakfastActive.value = false;
            isLunchActive.value = true;
            isDinnerActive.value = false;
            isSnackActive.value = false;
        }

        function activateDinner() {
            isBreakfastActive.value = false;
            isLunchActive.value = false;
            isDinnerActive.value = true;
            isSnackActive.value = false;
        }

        function activateSnack() {
            isBreakfastActive.value = false;
            isLunchActive.value = false;
            isDinnerActive.value = false;
            isSnackActive.value = true;
        }

        return { 
            isBreakfastActive, 
            isLunchActive, 
            isDinnerActive, 
            isSnackActive,
            listOfIgredients, 
            activateBreakfast,
            activateLunch, 
            activateDinner,
            activateSnack,
            addScrambledEggs,
            addSkyrPancakes,
            addEggSalad,
            addTofuPaste,
            addChickenPasta,
            addCheeseburger,
            addPancakes,
            addVegeNuggets,
            addChickenSalad,
            addCheeseSandwich,
            addTofuSalad,
            addSweetPotatos,
            addChips,
            addCarrotChips,
            addChocolate,
            addSticks,
            deleteChips,
            deleteCarrotChips,
            deleteChocolate,
            deleteSticks
        };
    }
}
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        flex-direction: column;
        align-items: center;
        padding: 15px 10%;
    }

    h3 {
        cursor: pointer;
    }

    ul {
        list-style: none;

    }

    li {
        display: inline-block;
        padding: 0px 50px;
    }
</style>