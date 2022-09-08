<template>
    <header>
        <h2>Shopping List Generator</h2>
        <nav>
            <ul>
                <li @click="activateBreakfast">Śniadania</li>
                <li @click="activateLunch">Obiady</li>
                <li @click="activateDinner">Kolacje</li>
                <li @click="activateSnack">Przekąski</li>
            </ul>
        </nav>
    </header>
    <div class="listDiv" id="listDivToPDF">
        <h3>Lista Zakupów</h3>
        <template v-for="product in listOfIgredients" :key="product">
            <p v-if="product.value > 0">{{product.polishWord}}: {{product.value}} {{product.unit}}</p>
        </template>
        <button @click="exportToPDF">Zapisz jako PDF</button>
    </div>

    <BreakfastComponent 
        class="section"
        v-show="isBreakfastActive" 
        @add-eggs-to-list=addScrambledEggs
        @add-skyr-pancakes-to-list=addSkyrPancakes
        @add-Egg-Salad-To-List=addEggSalad
        @add-Tofu-Paste-To-List=addTofuPaste
        @delete-Scrambled-Eggs-From-List=deleteScrambledEggs
        @delete-Skyr-Pancakes-From-List=deleteSkyrPancakes
        @delete-Egg-Salad-From-List=deleteEggSalad
        @delete-Tofu-Paste-From-List=deleteTofuPaste
    />

    <LunchComponent 
        class="section"
        v-show="isLunchActive"
        @add-Chicken-Pasta-To-List=addChickenPasta
        @add-Cheeseburger-To-List=addCheeseburger
        @add-Pancakes-To-List=addPancakes
        @add-Vege-Nuggets-To-List=addVegeNuggets
        @delete-Chicken-Pasta-From-List=deleteChickenPasta
        @delete-Cheeseburger-From-List=deleteCheeseburger
        @delete-Pancakes-From-List=deletePancakes
        @delete-Vege-Nuggets-From-List=deleteVegeNuggets
    />

    <DinnerComponent 
        class="section"
        v-show="isDinnerActive"
        @add-Chicken-Salad-To-List=addChickenSalad
        @add-Cheese-Sandwich-To-List=addCheeseSandwich
        @add-Tofu-Salad-To-List=addTofuSalad
        @add-Sweet-Potatos-To-List=addSweetPotatos
        @delete-Chicken-Salad-From-List=deleteChickenSalad
        @delete-Cheese-Sandwich-From-List=deleteCheeseSandwich
        @delete-Tofu-Salad-From-List=deleteTofuSalad
        @delete-Sweet-Potatos-From-List=deleteSweetPotatos
    />

    <SnackComponent 
        class="section"
        v-show="isSnackActive"
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
import html2pdf from 'html2pdf.js'

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
            onion:{ value: 0, polishWord: 'cebula', unit: 'g'},
            tomato:{ value: 0, polishWord: 'pomidory', unit: 'g'},
            roll:{ value: 0, polishWord: 'bułki', unit: 'szt.'},
            bacon: { value: 0, polishWord: 'bekon', unit: 'g'}, 
            cheese: { value: 0, polishWord: 'ser żółty', unit: 'g'},
            eggs: { value: 0, polishWord: 'jaja', unit: 'szt.'},
            beef: { value: 0, polishWord: 'wołowina', unit: 'g'},
            flour: { value: 0, polishWord: 'mąka', unit: 'g'},
            milk: { value: 0, polishWord: 'mleko', unit: 'ml'},
            curds: { value: 0, polishWord: 'serek wiejski', unit: 'g'},
            raisins: { value: 0, polishWord: 'rodzynki', unit: 'g'},
            vanillaSkyr: { value: 0, polishWord: 'skyr waniliowy', unit: 'g'},
            mayonnaise: { value: 0, polishWord: 'majonez', unit: 'g'},
            chives: { value: 0, polishWord: 'szczypiorek', unit: 'g'},
            tofu: { value: 0, polishWord: 'tofu', unit: 'g'},
            pasta: { value: 0, polishWord: 'makaron', unit: 'g'},
            chicken: { value: 0, polishWord: 'pierś z kurczaka', unit: 'g'},
            sweetPotato: { value: 0, polishWord: 'bataty', unit: 'g'},
            chickPeas: { value: 0, polishWord: 'ciecierzyca', unit: 'g'},
            breadCrumbs: { value: 0, polishWord: 'bułka tarta', unit: 'g'},
            sweetPepper: { value: 0, polishWord: 'papryka słodka', unit: 'g'},
            cucumber: { value: 0, polishWord: 'ogórki', unit: 'g'},
            chips: { value: 0, polishWord: 'chipsy', unit: 'op.'},
            carrotChips: { value: 0, polishWord: 'chipsy marchewkowe', unit: 'op.'},
            chocolate: { value: 0, polishWord: 'czekolada', unit: 'op.'},
            sticks: { value: 0, polishWord: 'paluszki', unit: 'op.'},
    });

        const addScrambledEggs = val => {
            val.count++
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.bacon.value += val.bacon;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
        }

        const addSkyrPancakes = val => {
            val.count++
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.vanillaSkyr.value += val.vanillaSkyr;
            listOfIgredients.flour.value += val.flour;
        }

        const addEggSalad = val => {
            val.count++
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.chives.value += val.chives;
        }

        const addTofuPaste = val => {
            val.count++
            listOfIgredients.tofu.value += val.tofu;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
        }

        const deleteScrambledEggs = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.eggs.value -= val.eggs;
                listOfIgredients.onion.value -= val.onion;
                listOfIgredients.bacon.value -= val.bacon;
                listOfIgredients.roll.value -= val.roll;
                listOfIgredients.tomato.value -= val.tomato;
            }
        }

        const deleteSkyrPancakes = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.eggs.value -= val.eggs;
                listOfIgredients.vanillaSkyr.value -= val.vanillaSkyr;
                listOfIgredients.flour.value -= val.flour;
            }
        }

        const deleteEggSalad = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.eggs.value -= val.eggs;
                listOfIgredients.mayonnaise.value -= val.mayonnaise;
                listOfIgredients.roll.value -= val.roll;
                listOfIgredients.chives.value -= val.chives;
            }
        }

        const deleteTofuPaste = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.tofu.value -= val.tofu;
                listOfIgredients.roll.value -= val.roll;
                listOfIgredients.tomato.value -= val.tomato;
            }
        }

        const addChickenPasta = val => {
            val.count++
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.pasta.value += val.pasta;
            listOfIgredients.chicken.value += val.chicken;
            listOfIgredients.cheese.value += val.cheese;
        }

        const addCheeseburger = val => {
            val.count++
            listOfIgredients.onion.value += val.onion;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.bacon.value += val.bacon;
            listOfIgredients.beef.value += val.beef;
            listOfIgredients.cheese.value += val.cheese;
        }

        const addPancakes = val => {
            val.count++
            listOfIgredients.flour.value += val.flour;
            listOfIgredients.eggs.value += val.eggs;
            listOfIgredients.milk.value += val.milk;
            listOfIgredients.curds.value += val.curds;
            listOfIgredients.raisins.value += val.raisins;
        }

        const addVegeNuggets = val => {
            val.count++
            listOfIgredients.sweetPotato.value += val.sweetPotato;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.breadCrumbs.value += val.breadCrumbs;
            listOfIgredients.sweetPepper.value += val.sweetPepper;
        }

        const deleteChickenPasta = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.onion.value -= val.onion;
                listOfIgredients.tomato.value -= val.tomato;
                listOfIgredients.pasta.value -= val.pasta;
                listOfIgredients.chicken.value -= val.chicken;
                listOfIgredients.cheese.value -= val.cheese;
            }
        }

        const deleteCheeseburger = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.onion.value -= val.onion;
                listOfIgredients.tomato.value -= val.tomato;
                listOfIgredients.roll.value -= val.roll;
                listOfIgredients.bacon.value -= val.bacon;
                listOfIgredients.beef.value -= val.beef;
                listOfIgredients.cheese.value -= val.cheese;
            }
        }

        const deletePancakes = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.flour.value -= val.flour;
                listOfIgredients.eggs.value -= val.eggs;
                listOfIgredients.milk.value -= val.milk;
                listOfIgredients.curds.value -= val.curds;
                listOfIgredients.raisins.value -= val.raisins;
            }
        }

        const deleteVegeNuggets = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.sweetPotato.value -= val.sweetPotato;
                listOfIgredients.chickPeas.value -= val.chickPeas;
                listOfIgredients.breadCrumbs.value -= val.breadCrumbs;
                listOfIgredients.sweetPepper.value -= val.sweetPepper;
            }
        }

        const addChickenSalad = val => {
            val.count++
            listOfIgredients.chicken.value += val.chicken;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
            listOfIgredients.chives.value += val.chives;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
        }

        const addCheeseSandwich = val => {
            val.count++
            listOfIgredients.cheese.value += val.cheese;
            listOfIgredients.roll.value += val.roll;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
        }

        const addTofuSalad = val => {
            val.count++
            listOfIgredients.tofu.value += val.tofu;
            listOfIgredients.chickPeas.value += val.chickPeas;
            listOfIgredients.tomato.value += val.tomato;
            listOfIgredients.cucumber.value += val.cucumber;
            listOfIgredients.chives.value += val.chives;
            listOfIgredients.mayonnaise.value += val.mayonnaise;
        }

        const addSweetPotatos = val => {
            val.count++
            listOfIgredients.sweetPotato.value += val.sweetPotato;
            listOfIgredients.tomato.value += val.tomato;
        }




        const deleteChickenSalad = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.chicken.value -= val.chicken;
                listOfIgredients.chickPeas.value -= val.chickPeas;
                listOfIgredients.tomato.value -= val.tomato;
                listOfIgredients.cucumber.value -= val.cucumber;
                listOfIgredients.chives.value -= val.chives;
                listOfIgredients.mayonnaise.value -= val.mayonnaise;
            }
        }

        const deleteCheeseSandwich = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.cheese.value -= val.cheese;
                listOfIgredients.roll.value -= val.roll;
                listOfIgredients.tomato.value -= val.tomato;
                listOfIgredients.cucumber.value -= val.cucumber;
            }
        }

        const deleteTofuSalad = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.tofu.value -= val.tofu;
                listOfIgredients.chickPeas.value -= val.chickPeas;
                listOfIgredients.tomato.value -= val.tomato;
                listOfIgredients.cucumber.value -= val.cucumber;
                listOfIgredients.chives.value -= val.chives;
                listOfIgredients.mayonnaise.value -= val.mayonnaise;
            }
        }

        const deleteSweetPotatos = val => {
            if(val.count > 0) {
                val.count--;
                listOfIgredients.sweetPotato.value -= val.sweetPotato;
                listOfIgredients.tomato.value -= val.tomato;
            }
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
            if(listOfIgredients.chips.value > 0) {
                listOfIgredients.chips.value--
            }
        }

        const deleteCarrotChips = () => {
            if(listOfIgredients.carrotChips.value > 0) {
                listOfIgredients.carrotChips.value--
            }
        }

        const deleteChocolate = () => {
            if(listOfIgredients.chocolate.value > 0) {
                listOfIgredients.chocolate.value--
            }
        }

        const deleteSticks = () => {
            if(listOfIgredients.sticks.value > 0) {
                listOfIgredients.sticks.value--
            }
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

        function exportToPDF() {
            html2pdf(document.getElementById('listDivToPDF'), {
                margin: 2,
                filename: "lista zakupów.pdf",
            });
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
            deleteScrambledEggs,
            addSkyrPancakes,
            deleteSkyrPancakes,
            addEggSalad,
            deleteEggSalad,
            addTofuPaste,
            deleteTofuPaste,
            addChickenPasta,
            deleteChickenPasta,
            addCheeseburger,
            deleteCheeseburger,
            addPancakes,
            deletePancakes,
            addVegeNuggets,
            deleteVegeNuggets,
            addChickenSalad,
            deleteChickenSalad,
            addCheeseSandwich,
            deleteCheeseSandwich,
            addTofuSalad,
            deleteTofuSalad,
            addSweetPotatos,
            deleteSweetPotatos,
            addChips,
            deleteChips,
            addCarrotChips,
            deleteCarrotChips,
            addChocolate,
            deleteChocolate,
            addSticks,
            deleteSticks,
            exportToPDF
        };
    }
}
</script>

<style scoped>
    header {
        grid-area: 1 / 2 / 2 / 7;
        background-color: rgb(63, 63, 63);
        /* background: linear-gradient(to bottom right, red, rgb(63, 63, 63), rgb(63, 63, 63)); */
    }

    h2 {
        margin: 0;
    }

    h3 {
        cursor: pointer;
    }

    nav {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    ul {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        list-style: none;
        padding: 0;
    }

    li {
        cursor: pointer;
        margin: 5%;
        border: 2px black solid;
    }

    .listDiv {
        grid-area: 1 / 1 / 7 / 2;
        background-color: rgb(63, 63, 63);
        padding: 0;
        /* display:flex;
         border:3px solid black;
         flex-direction:column;
         flex-wrap:wrap;
         width: 80%;
         height: 100%; */

    }

    .listDiv > p {
        display: flex;
        flex-wrap: wrap;
        flex-flow: column wrap;
        margin: 0;
    }

    .section {
        grid-area: 2 / 2 / 7 / 7;


    }

</style>