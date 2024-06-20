<script setup>
import { ref, computed, onUpdated } from "vue";
import Header from "./Header.vue";
import BarraSalute from "./BarraSalute.vue";
import Button from "./Button.vue";
import Win from "./Win.vue"

const round = ref(0);

const saluteNemico = ref(100);
const salutePlayer = ref(100);

const numberRandom = (max, min) => {
    return Math.floor(Math.random() * (max - min)) + min;
}

const attackPlayer = () => {
    salutePlayer.value -= numberRandom(10, 5);
}

const attackNemico = () => {
    saluteNemico.value -= numberRandom(10, 5);
}

const playerStyle = computed(() => {
    return {
        "width": `${salutePlayer.value}%`
    }
})

const nemicoStyle = computed(() => {
    return {
        "width": `${saluteNemico.value}%`
    }
})


const attack = () => {
    round.value++;
    attackPlayer()
    attackNemico()
}

const attaccoSpeciale = () => {
    round.value++;
    salutePlayer.value -= numberRandom(15, 10);
    saluteNemico.value -= numberRandom(15, 10);
}

const onMedikit = () => {
    round.value++;
    salutePlayer.value += numberRandom(10, 5);
    attackPlayer()
}

const metaSalute = salutePlayer.value / 2;

const disabled = ref(true);

const win = ref(false);

const winner = ref("");


onUpdated(() => {
    if (salutePlayer.value < metaSalute && round.value % 3 === 0) {
        disabled.value = false
    }
    else {
        disabled.value = true
    }

    winGame()
})

const winGame = () => {
    if (salutePlayer.value <= 0 || saluteNemico.value <= 0) {
        win.value = true;

        if (salutePlayer.value < saluteNemico.value) {
            winner.value = "Hai perso!"
        }
        else if (salutePlayer.value > saluteNemico.value) {
            winner.value = "Hai vinto!";
        }
        else {
            winner.value = "Pareggio!"
        }
    }
}

const handeNewGame = () => {
    win.value = false;
    console.log(win.value);
}



</script>




<template>

    <Header :round="round"></Header>

    <div class="container">

        <div class="game">

            <Win v-if="win" :msgWin="winner" @newGame="handeNewGame()"></Win>

            <div v-if="!win">

                <BarraSalute player="Tu" :salute="salutePlayer" :styleSalute="playerStyle"></BarraSalute>

                <BarraSalute player="Nemico" :salute="saluteNemico" :styleSalute="nemicoStyle"></BarraSalute>

                <section class="buttons">
                    <Button title="Attacco" @click="attack()" classe="attacco"></Button>
                    <Button title="Attacco Speciale" @click="attaccoSpeciale()" classe="attacco-speciale"
                        :disabled="round === 0 || round % 3 !== 0"></Button>
                    <Button title="Medikit" :disabled="disabled" @click="onMedikit()" classe="medikit"></Button>
                    <Button title="Mi arrendo!" @click="salutePlayer = 0" classe="mi-arrendo"></Button>
                </section>

            </div>
        </div>
    </div>
</template>


<style scoped>
.container {
    display: flex;
}

.game {
    width: 1000px;
    margin: 0 auto;
}

section.buttons {
    margin: 20px 0;
    display: flex;
    flex-wrap: wrap;
    width: 100%;
    justify-content: space-between;
}
</style>