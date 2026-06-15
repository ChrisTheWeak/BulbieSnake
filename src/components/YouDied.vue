<template>
<Teleport to="body">
<div class="modal-box">
    <div class="modal" style="width:20%; height:auto; padding: 5px; text-align: center;">
        <h1 style="margin-block:0px;">YOU DIED!</h1>
        <div style="display: grid;">
            <img style="margin-inline:auto" src="/dead.png">
        </div>
        <h3>Press Enter or refresh the page to restart</h3>
    </div>
</div>
</Teleport>
</template>



<script setup lang="ts">
import { useGamestate } from '@/GameState';
import { Teleport } from 'vue';

addEventListener('keydown', (ev) => {
    if (ev.key === 'Enter') {
        useGamestate().start()
    }
})
</script>