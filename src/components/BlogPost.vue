<script setup>
defineProps({
    id: Number,
    title: String,
    body: {
        type: String,
        default: "Sin descripción"
    },
    colorText: String
});

const emit = defineEmits(['favPost'])
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">{{ id }} - {{ title }}</h5>
            <p>{{ body }}</p>
            <button @click="emit('favPost', title)" 
            class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>