<template>
    <header>
        <h2>Shopping List Generator</h2>
        <nav>
            <ul>
                <li @click="activateBreakfast" :class="{activeSection: isBreakfastActive}">Śniadania</li>
                <li @click="activateLunch" :class="{activeSection: isLunchActive}">Obiady</li>
                <li @click="activateDinner" :class="{activeSection: isDinnerActive}">Kolacje</li>
                <li @click="activateSnack" :class="{activeSection: isSnackActive}">Przekąski</li>
                <li @click="isListDivActive=!isListDivActive" :class="{activeSection: isListDivActive}">Lista Zakupów</li>
            </ul>
        </nav>
    </header>
    <transition-group name="showList" mode="out-in">
        <div v-if="isListDivActive" class="listDiv" :class="{white: isWhite, dark: isDark}" id="listDivToPDF">
            <h3>Lista Zakupów</h3>
            <button @click="exportToPDF" data-html2canvas-ignore>Zapisz jako PDF</button>
            <button @click="isListDivActive=!isListDivActive" data-html2canvas-ignore>Zamknij</button>
            <template v-for="product in listOfIgredients" :key="product">
            <p v-if="product.value > 0">{{product.polishWord}}: {{product.value}} {{product.unit}}</p>
            </template>
        </div>
    
    
        <BreakfastComponent 
            class="section"
            :key="1"
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
            :key="2"
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
            :key="3"
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
            :key="4"
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
    </transition-group>
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
        const isListDivActive = ref(false);
        const isWhite = ref(false);
        const isDark = ref(true)

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






        const addChips = val => {
            val.count++;
            listOfIgredients.chips.value++
        }

        const addCarrotChips = val => {
            val.count++;
            listOfIgredients.carrotChips.value++
        }

        const addChocolate = val => {
            val.count++;
            listOfIgredients.chocolate.value++
        }

        const addSticks = val => {
            val.count++;
            listOfIgredients.sticks.value++
        }

        const deleteChips = val => {
            if(listOfIgredients.chips.value > 0) {
                val.count--;
                listOfIgredients.chips.value--
            }
        }

        const deleteCarrotChips = val => {
            if(listOfIgredients.carrotChips.value > 0) {
                val.count--;
                listOfIgredients.carrotChips.value--
            }
        }

        const deleteChocolate = val => {
            if(listOfIgredients.chocolate.value > 0) {
                val.count--;
                listOfIgredients.chocolate.value--
            }
        }

        const deleteSticks = val => {
            if(listOfIgredients.sticks.value > 0) {
                val.count--;
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
            isWhite.value = true;
            isDark.value = false;
            html2pdf(document.getElementById('listDivToPDF'), {
                filename: "lista zakupów.pdf",
                margin: 5,
            });
            setTimeout(function() {
                isWhite.value = false;
                isDark.value = true;
            }, 200);
            
        }

        return { 
            isBreakfastActive, 
            isLunchActive, 
            isDinnerActive, 
            isSnackActive,
            isListDivActive,
            isWhite,
            isDark,
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
        grid-area: 1 / 1 / 2 / 7;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
        background-color: rgb(37, 36, 36);
        
    }

    h2 {
        margin: 0;
    }

    h3 {
        cursor: pointer;
    }

    nav {
        display: flex;
        justify-content: center;
    }

    ul {
        display: flex;
        justify-content: center;
        align-items: center;
        list-style: none;
        padding: 0;
        margin: 0 0 0 0;
    }

    li {
        cursor: pointer;
        margin: 2%;
        background-color: rgb(20, 20, 20);
        border-radius: 15px;
        padding: 0 2.5rem 0 2.5rem;
        transition-duration: 0.1s;
    }

    .listDiv {
        grid-area: 1 / 3 / 7 / 5;
        padding: 0;
        z-index: 1;
    }

    li:hover {
        color: rgb(20, 20, 20);
        background-color: rgb(238,8,8, 0.8);
    }

    li:active {
        background-color:rgba(19, 155, 17, 0.753);
    }

    .listDiv > p {
        display: flex;
        flex-wrap: wrap;
        flex-flow: column wrap;
        margin: 0;
    }

    .showList-enter-active, .showList-leave-active {
        transition: opacity 1s ease;
    }

    .showList-enter-from, .showList-leave-to {
        opacity: 0;
    }

    .showList-leave-from, .showList-enter-to {
        opacity: 1;
    }

    .activeSection {
        background-color: rgb(238,8,8, 0.8);
        color: rgb(20, 20, 20);
    }

    .section {
        grid-area: 2 / 1 / 7 / 7;
    }

    .white {
        background-color: rgb(255, 255, 255);
        transition: 0.2s;
    }

    .dark {
        background-color: rgb(37, 36, 36);
        transition: 0.2s;
    }


    @media (orientation: portrait) {
        ul {
            display: flex;
            flex-direction: column;
        }

        li {
            margin: 0.5%;
            background-color: rgb(20, 20, 20);
            border-radius: 15px;
            padding: 0 2.5rem 0 2.5rem;
            width: 6rem;
            font-size: 0.8rem;
        }

        .listDiv {
        grid-area: 1 / 2 / 7 / 6;
        }
    }

</style>