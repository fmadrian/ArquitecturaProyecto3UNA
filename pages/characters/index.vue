<!-- pages/authors_index.vue -->
<template>
    <div class="container">
        <HeaderView />
        <div>
            {{ items }}
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const items = (await queryContent('/characters').only('body').findOne()).body;
</script>