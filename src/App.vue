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
            <div class="game-btns" v-if="result === -3">
                <input class="btn" id="rock-btn" @click="move('rock')" type="image" src="./src/assets/images/icon-rock.svg" />
                <input class="btn" id="paper-btn" @click="move('paper')" type="image" src="./src/assets/images/icon-paper.svg" />
                <input class="btn" id="scissors-btn" @click="move('scissors')" type="image" src="./src/assets/images/icon-scissors.svg" />
            </div>
            <div class="result" v-if="result !== -3">
                <div class="move">
                    <div class="move-title">ВЫ</div>
                    <div v-if="playerMove === 'rock'"><img class="btn rock" src="./assets/images/icon-rock.svg"></div>
                    <div v-if="playerMove === 'paper'"><img class="btn paper" src="./assets/images/icon-paper.svg"></div>
                    <div v-if="playerMove === 'scissors'"><img class="btn scissors" src="./assets/images/icon-scissors.svg"></div>
                </div>
                <div class="res">
                    <div class="res-body" v-if="result === 1">
                        ВЫ ПОБЕДИЛИ
                    </div>
                    <div class="res-body" v-else-if="result === 0">
                        НИЧЬЯ
                    </div>
                    <div class="res-body" v-else-if="result === -1">
                        ВЫ ПРОИГРАЛИ
                    </div>
                    <button @click="restartGame" class="play-again">ИГРАТЬ СНОВА</button>
                </div>
                <div class="move">
                    <div class="move-title">КОМПЬЮТЕР</div>
                    <div v-if="computerMove === 'rock'"><img class="btn rock" src="./assets/images/icon-rock.svg"></div>
                    <div v-if="computerMove === 'paper'"><img class="btn paper" src="./assets/images/icon-paper.svg"></div>
                    <div v-if="computerMove === 'scissors'"><img class="btn scissors" src="./assets/images/icon-scissors.svg"></div>
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
    function restartGame() {
        result.value = -3;
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
    .rock{ border: 10px solid red; }
    .paper{ border: 10px solid dodgerblue; }
    .scissors{ border: 10px solid coral; }
    #rock-btn {
        border: 10px solid red;
    }
    #paper-btn {
        border: 10px solid dodgerblue;
        position: absolute;
        right: 0;
    }
    #scissors-btn {
        border: 10px solid coral;
        position: absolute;
        left: 35%;
        bottom: 0;
    }
    .game-btns {
        margin: 10px;
        background-image: url("./assets/images/bg-triangle.svg");
        background-repeat: no-repeat;
        background-size: auto;
        background-position: center;
        height: 45vh;
        width: 50vh;
        position: relative;
    }

    .result {
        display: flex;
        align-items: center;
    }
    .res-body {
        margin: 10px 30px;
        color: white;
        font-size: 3vh;
    }
    .res {
        display: flex;
        flex-flow: column;
        align-items: center;
        margin: 2vh;
    }
    .res button {
        border: none;
        background-color: white;
        border-radius: 10px;
        height: 5vh;
        width: 20vh;
        color: #264174;
    }
    .res button:hover {
        cursor: pointer;
    }
    .move-title {
        color: white;
    }
    .move {
        display: flex;
        flex-flow: column;
        align-items: center;
    }
</style>