<script setup>

const props = defineProps({
    msgWin: {
        type: String,
        required: false
    }
})

const emit = defineEmits(["newGame"])

const newGame = () => {
    emit('newGame')
}

</script>



<template>

    <div class="game-over">

        <h1>Game Over!</h1>

        <p>{{ msgWin }}</p>

        <button @click="newGame()">Nuovo Gioco</button>

    </div>


</template>



<style scoped>

.game-over{
    border: 1px solid rgba(0, 0, 0, 0.523);
    border-radius: 10px;
    padding: 20px;
    text-align: center
}

.game-over button{
    background-color: blue;
    color: white;
    padding: 15px;
    cursor: pointer;
    outline: none;
    border-radius: 10px;
    border: none;
}

</style>