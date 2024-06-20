<script setup>

    import { ref } from "vue";

    const props = defineProps({
        player: {
            type: String,
            required: true
        },
        salute: {
            type: Number,
            required: false
        },
        styleSalute: {
            type: Object,
            required: false
        }
    })

    
</script>



<template>
    <section class="punti">
        <p>{{ props.player }} ({{ props.salute }})</p>
        <div class="puntiVita" :style="styleSalute">

        </div>
    </section>
</template>


<style scoped>
    section.punti{
        border: 1px solid rgba(0, 0, 0, 0.251);
        border-radius: 7px;
        padding: 20px;
        margin: 20px 0;
    }

    p{
            text-align: center;
    }

    .puntiVita{
        background-color: red;
        height: 30px
    }

</style>