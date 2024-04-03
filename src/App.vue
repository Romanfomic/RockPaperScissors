<template>
    <div>
        <div class="game">
            <div class="game-btns" v-for="item in items" :key="item">
                <button @click="move(item)">{{ item }}</button>
            </div>
            <div class="player-move">{{ playerMove }}</div>
            <div class="computer-move">{{ computerMove }}</div>
            <div class="res" v-if="result === 1 || result === -2">
                Вы победили
            </div>
            <div class="res" v-else-if="result === 0">
                Ничья
            </div>
            <div class="res" v-else-if="result === -1">
                Вы проиграли
            </div>
        </div>
    </div>
</template>

<script setup>
    import { ref, computed } from 'vue'
    const items = ["Rock", "Paper", "Scissors"];
    const playerMove = ref("");
    const computerMove = ref("");
    const result = ref(-3);
    function move(arg) {
        playerMove.value = arg;
        let randomIndex = Math.floor(Math.random() * 3);
        computerMove.value = items[randomIndex];

        result.value = items.indexOf(playerMove.value) - items.indexOf(computerMove.value);
    }
</script>

<style>

</style>