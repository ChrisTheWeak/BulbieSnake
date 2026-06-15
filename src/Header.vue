<template>
    <div class="dark" style="height:60px; display:flex">
        <div class="light" style="margin:10px; padding-block:5px; flex-grow:1; display:flex;">
            <img id="food-counter" style="margin-left:20px;" src="/food.png"></img>
            <label for="food-counter" style="font-size:calc(100% + 10px);">{{ eaten }}</label>
        </div>
    </div>
</template>

<script setup lang="ts">
import { useGamestate } from './GameState';

const eaten = useGamestate().eaten
</script>