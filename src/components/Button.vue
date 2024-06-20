<script setup>

const props = defineProps({
    title: {
        type: String,
        required: true
    },
    classe: {
        type: String,
        required: false
    },
})


</script>



<template>

    <button :class="classe">{{ props.title }}</button>

</template>


<style scoped>
button {
    width: calc(98% / 2);
    margin: 10px 0;
    padding: 10px;
    color: white;
    border-radius: 7px;
    border: none;
    cursor: pointer;
}

.attacco {
    background-color: blue;
}

.attacco-speciale {
    background-color: blue;
}

.medikit {
    background-color: red;
}

.mi-arrendo {
    background-color: red;
}

:disabled {
    background-color: gray;
    cursor: no-drop;
}
</style>