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
        <p>{{listOfIgredients.bacon}}</p>
        <p>{{listOfIgredients.eggs}}</p>
        <p>{{listOfIgredients.roll}}</p>
    </div>
  </header>
    <BreakfastComponent 
        v-if="isBreakfastActive" 
        @add-eggs-to-list=addScrambledEggs
        @add-skyr-pancakes-to-list=addSkyrPancakes
    />


  <LunchComponent v-if="isLunchActive"/>
  <DinnerComponent v-if="isDinnerActive"/>
  <SnackComponent v-if="isSnackActive"/>
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
            vanillaSkyr: 0,
            mayonnaise: 0,
            chives: 0,
            tofu: 0,
            pasta: 0,
            chicken: 0,
            sweetPotato: 0,
            chickPeas: 0,
            breadCrumbs: 0,
            sweetPepper: 0,
            cucumber: 0,
            chips: 0,
            carrotChips: 0,
            chocolate: 0,
            sticks: 0,
    });

        const addScrambledEggs = val => {
            listOfIgredients.eggs += val.eggs;
            listOfIgredients.onion += val.onion;
            listOfIgredients.bacon += val.bacon;
            listOfIgredients.roll += val.roll;
            listOfIgredients.tomato += val.tomato;
            console.log(listOfIgredients.eggs);
            console.log(listOfIgredients.onion);
            console.log(listOfIgredients.bacon);
            console.log(listOfIgredients.roll);
            console.log(listOfIgredients.tomato);
        }

        const addSkyrPancakes = val => {
            listOfIgredients.eggs += val.eggs;
            listOfIgredients.vanillaSkyr += val.eggs;
            listOfIgredients.flour += val.flour;
            console.log(listOfIgredients.flour);
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
            addSkyrPancakes
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