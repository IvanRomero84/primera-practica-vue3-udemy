<template>
    <div class="card">
        <div class="card-body">
            <h5 :class="`text-${colorText}`" class="card-title" >{{id}} - {{title}}</h5>
            <p>{{body}}</p>
            <button class="btn btn-outline-primary" @click="emit('cambiarFavoritoNombre', title)">Favorito</button>
        </div>
    </div>
</template>

<script setup>
// defineProps(['title', 'id', 'description', 'colorText'])
defineProps({
    title: String,
    id: Number,
    body: {
        type: String,
        default: 'Sin descripción'
    },
    colorText: String,
})
const emit = defineEmits(['cambiarFavoritoNombre'])
</script>