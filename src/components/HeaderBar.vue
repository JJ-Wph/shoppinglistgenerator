<template>
  <header>
    <h3>Shopping List Generator</h3>
    <nav>
        <ul>
            <li>Śniadania</li>
            <li>Obiady</li>
            <li>Kolacje</li>
            <li>Przekąski</li>
        </ul>
    </nav>
    <div class="recipeDiv">
        <p>{{listOfIgredients.bacon}}</p>
        <p>{{listOfIgredients.eggs}}</p>
        <p>{{listOfIgredients.roll}}</p>
    </div>
  </header>
</template>

<script>
import {reactive} from 'vue'
export default {
    name: 'HeaderBar',
    setup(){
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

        return {listOfIgredients}
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