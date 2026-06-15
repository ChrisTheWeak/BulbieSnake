<template>
  <header>
    <Header></Header>
  </header>
  <YouDied v-if="useGamestate().state.value === Playstate.Dead" />
  <YouWon v-if="useGamestate().state.value === Playstate.Won" />
  <TheGame></TheGame>
</template>

<script setup lang="ts">
import YouDied from './components/YouDied.vue';
import YouWon from './components/YouWon.vue';
import { Direction, opposite, Playstate, useGamestate } from './GameState.js';
import Header from './Header.vue';
import TheGame from './TheGame.vue';

function getDirectionFromKey(key: string): Direction | undefined {
  switch(key) {
  case 'ArrowLeft':
  case 'a':
  case 'A':
    return Direction.Left
  case 'ArrowRight':
  case 'd':
  case 'D':
    return Direction.Right
  case 'ArrowUp':
  case 'w':
  case 'W':
    return Direction.Up
  case 'ArrowDown':
  case 's':
  case 'S':
    return Direction.Down
  default:
    return undefined
  }
}


addEventListener('keydown', async (ev: KeyboardEvent) => {
  if (ev.key === 'Enter') {
    useGamestate().start()
    return
  }
  if (ev.key === ' ') {
    useGamestate().usingFastTickrate.value = true
  }
  const direction = getDirectionFromKey(ev.key)
  if (direction == null) return
  useGamestate().pointTo(direction)
  // If we are trying to point ourselves back into ourselves, just don't do that
})
addEventListener('keyup', (ev: KeyboardEvent) => {
  if (ev.key === ' ') {
    useGamestate().usingFastTickrate.value = false
  }
})
</script>