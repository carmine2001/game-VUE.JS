<script setup>
    const props = defineProps({
        round: {
            type: Number,
            required: false
        }
    })
</script>



<template>
    <header>
        <h1>Game ({{ props.round }})</h1>
    </header>
</template>


<style scoped>
    header{
    background-color: green;
}
h1{
        color: white;
        text-align: center;
    }
</style>