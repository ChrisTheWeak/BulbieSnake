<template>
    <div class="bg" style="height:100%;padding:auto;flex-shrink:1;min-width:0;display:flex;">
        <div class="game-wrapper">
            <div class="game-grid">
                <template v-for="row in game.rows">
                    <template v-for="column in game.columns">
                        <div :class="row % 2 != column % 2 ? 'dark' : 'light'">
                            <SnakeCell :pos="{ y: row, x: column }"/>
                        </div>
                    </template>
                </template>
            </div>
        </div>
    </div>
</template>

<style scoped>
.game-grid {
    display:grid;
    grid-template-columns: repeat(35, minmax(0, 1fr));
    grid-template-rows: repeat(15, minmax(0, 1fr));
    aspect-ratio:calc(35/15);
    margin:auto;
}
.game-wrapper {
    margin:auto;
}
</style>

<script setup lang="ts">
import SnakeCell from './components/SnakeCell.vue';
import { useGamestate } from './GameState';

const game = useGamestate();

</script>