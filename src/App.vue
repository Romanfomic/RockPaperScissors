<template>
    <div>
        <div class="game">
            <div class="score-panel">
                <img src="./assets/images/logo.svg">
                <div class="score">
                    <div class="score-title">Счет</div>
                    <div class="score-body">{{ score }}</div>
                </div>
            </div>
            <div class="game-btns">
                <input class="btn" id="rock-btn" @click="move('rock')" type="image" src="./src/assets/images/icon-rock.svg" />
                <input class="btn" id="paper-btn" @click="move('paper')" type="image" src="./src/assets/images/icon-paper.svg" />
                <input class="btn" id="scissors-btn" @click="move('scissors')" type="image" src="./src/assets/images/icon-scissors.svg" />
            </div>
            <div class="result" v-if="result !== -3">
                <div class="player-move">{{ playerMove }}</div>
                <div class="computer-move">{{ computerMove }}</div>
                <div class="res" v-if="result === 1">
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
    </div>
</template>

<script setup>
    import { ref, computed } from 'vue'
    const items = ["rock", "paper", "scissors"];
    const playerMove = ref("");
    const computerMove = ref("");
    const result = ref(-3);
    const score = ref(0);
    function move(arg) {
        playerMove.value = arg;
        let randomIndex = Math.floor(Math.random() * 3);
        computerMove.value = items[randomIndex];

        result.value = items.indexOf(playerMove.value) - items.indexOf(computerMove.value);
        if (result.value < -1) result.value = 1;
        if (result.value > 1) result.value = -1;
        score.value += result.value;
    }
</script>

<style>
    body {
        background-color: #264174;
    }
    .game {
        display: flex;
        flex-flow: column;
        align-items: center;
    }

    .score-panel {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 300px;
        border: 2px solid rgba(255, 255, 255, 0.3);
        border-radius: 10px;
        padding: 10px;
        margin: 20px 0;
    }
    .score-panel img {
        height: 60px;
    }
    .score {
        display: flex;
        flex-flow: column;
        align-items: center;
        background-color: white;
        padding: 5px 20px;
        border-radius: 10px;
    }
    .score-body {
        font-weight: bold;
        font-size: 30px;
    }

    .btn {
        padding: 20px;
        margin: 10px;
        background-color: white;
        border-radius: 50px;
        width: 30px;
        height: 30px;
    }
    #rock-btn { border: 10px solid red; }
    #paper-btn { border: 10px solid dodgerblue; }
    #scissors-btn { border: 10px solid coral; }
</style>