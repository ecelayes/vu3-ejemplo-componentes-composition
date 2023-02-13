<script setup>
defineProps(["start", "end", "maxLength"]);

//const emit = defineEmits(['prevPage', 'nextPage'])
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
    <button 
        @click="$emit('prevPage')" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled="start <= 0"
    >
        Prev
    </button>
    <button 
        @click="$emit('nextPage')" 
        type="button" 
        class="btn btn-outline-primary"
        :disabled="end >= maxLength"
    >
        Next
    </button>
</div>
</template>