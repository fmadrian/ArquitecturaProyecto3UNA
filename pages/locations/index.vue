<!-- pages/authors_index.vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3">
                <h3>Ubicaciones</h3>
                <table class="table table-responsive table-primary table-striped table-bordered">
                    <thead>
                        <tr>
                            <th scope="col">Nombre</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(item, index) in items" :key="index">
                            <td>
                                <NuxtLink
                                    :to="{ name: 'locations-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-decoration-none">
                                    {{ item.name }}
                                </NuxtLink>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const items = (await queryContent('/locations').only('body').findOne()).body;
</script>