<template>
    <NuxtLink class="text-decoration-none" :to=to>
        <div class="card ">
            <img class="card-img-top" :src=src :alt=title>
            <div class="card-body">
                <h5 class="card-title">{{ title }}</h5>
            </div>
        </div>
    </NuxtLink>
</template>

<script setup>

const props = defineProps({
    title: {
        type: String,
        required: true
    },
    src: {
        type: String,
        required: true
    },
    to: {
        type: String,
        required: true
    }
})

</script>