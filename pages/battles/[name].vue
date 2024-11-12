<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-4 gx-4">
            {{ item }}
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const route = useRoute()

const item = (await queryContent('/battles').only('body').findOne()).body
    .find(item => item.name.trim() === route.params.name.trim())

</script>