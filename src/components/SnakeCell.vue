<template>
    <img class="snakeImage" v-if="hasFood" src="/food.png">
    <template v-else-if="thisType">
        <img class="snakeImage" v-if="thisType.toNext == null" src="/head.png" 
            :style="`transform: rotate(${thisType.toMe! * 90}deg)`">
        <img class="snakeImage" v-else-if="thisType.toMe == null" src="/tail.png" 
            :style="`transform: rotate(${thisType.toNext! * 90}deg)`">
        <img class="snakeImage" v-else-if="thisType.toMe === thisType.toNext" src="/body.png"
            :style="`transform: rotate(${thisType.toNext * 90}deg)`" >
        <img class="snakeImage" v-else src="/corner.png"
            :style="`transform: rotate(${(isTurnedRight(thisType.toMe, thisType.toNext) ? thisType.toNext : thisType.toMe - 2) * 90}deg)`">
    </template>
</template>

<style scoped>
.snakeImage {
    width: 100%;
    height: 100%;
}
</style>


<script setup lang="ts">
import { compare, Direction, eq, useGamestate, type Position } from '@/GameState';
import { computed } from 'vue';

const props = defineProps<{
    pos: Position
}>()

const gamestate = useGamestate()
const hasFood = computed(() => eq(props.pos, gamestate.food.value))
const snakeIndex = computed(() => gamestate.positions.value.findIndex((b) => eq(props.pos, b)))

function isTurnedRight(toMe: Direction, toNext: Direction) {
    return toMe === ((toNext + 1) % 4)
}

const thisType = computed<{toMe: Direction | undefined, toNext: Direction | undefined} | undefined>(() => {
    const index = snakeIndex.value
    if (index === -1) {
        return undefined
    }
    const lastIndex = gamestate.positions.value.length - 1
    const item = gamestate.positions.value[index]!
    const prevItem = index > 0 ? gamestate.positions.value[index - 1] : undefined
    const nextItem = index < lastIndex ? gamestate.positions.value[index + 1] : undefined

    let toMe = prevItem ? compare(prevItem, item) : undefined
    let toNext = nextItem ? compare(item, nextItem) : undefined
    if (toMe == null && toNext == null) {
        console.error("Failed to get any adjacent items", item, lastIndex, gamestate.positions.value)
        return undefined
    }
    return {
        toMe, // If a previous does not exist, we are the tail, so we can ignore this
        toNext, // Ditto
    }
})
</script>