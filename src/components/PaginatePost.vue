<template>
<div class="btn-group" role="group" aria-label="Basic example">
  <button type="button" class="btn btn-outline-primary" @click="emit('previous')" :disabled="inicio <= 0">Previous</button>
  <button type="button" class="btn btn-outline-primary" @click="emit('next')" :disabled="fin >= postsLength">Next</button>
</div>
</template>

<script setup>
defineProps({
    inicio: Number,
    fin: Number,
    postsLength: Number,
})
const emit = defineEmits(['next', 'previous'])
</script>