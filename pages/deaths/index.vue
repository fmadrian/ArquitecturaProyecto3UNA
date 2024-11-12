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
const items = (await queryContent('/deaths').only('body').findOne()).body;
</script>