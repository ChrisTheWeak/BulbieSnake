<template>
    <div class="bg" style="min-height:0px;padding:auto;flex-shrink:1;min-width:0;display:flex;flex-direction:column">
        <!-- <div class="game-wrapper"> -->
            <div class="game-grid" :style="gridTemplate">
                <template v-for="row in game.rows">
                    <template v-for="column in game.columns">
                        <div :class="row % 2 != column % 2 ? 'dark' : 'light'">
                            <SnakeCell :pos="{ y: row, x: column }"/>
                        </div>
                    </template>
                </template>
            </div>
        <!-- </div> -->
    </div>
</template>

<style scoped>
.game-grid {
    display:grid;
    margin:auto;
    min-width:0px;
    min-height:0px;
}
.game-wrapper {
    margin:auto;
}
</style>

<script setup lang="ts">
import { computed, type StyleValue } from 'vue';
import SnakeCell from './components/SnakeCell.vue';
import { useGamestate } from './GameState';

const game = useGamestate();

const gridTemplate = computed<StyleValue>(() => ({
    gridTemplateColumns: "minmax(0, 1fr) ".repeat(game.columns),
    gridTemplateRows: "minmax(0, 1fr) ".repeat(game.rows),
    aspectRatio: (game.columns / game.rows)
}))
</script>