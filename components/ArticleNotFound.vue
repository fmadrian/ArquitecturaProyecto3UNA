<template>
    <div class="container">
        <div class="d-flex flex-column row-gap-4">
            <div class="d-flex flex-column justify-items-center row-gap-3 text-center">
                <span class="fs-2">404</span>
                <h1>{{ itemType }} no encontrada(o)</h1>
                <NuxtLink :to=to>Volver a {{ text }}</NuxtLink>
                <NuxtLink to="/">Volver a página principal</NuxtLink>
            </div>
        </div>
    </div>
</template>
<script setup>
const props = defineProps({
    itemType: {
        type: String,
        default: "Artículo"
    },
    to: {
        type: String,
        default: "/"
    }, text: {
        type: String,
        default: "inicio"
    }
})
</script>