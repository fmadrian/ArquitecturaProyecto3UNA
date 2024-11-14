<!-- pages/authors_index.vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3">
                <h3>Batallas</h3>
                <table class="table table-responsive table-primary table-striped table-sm">
                    <thead>
                        <tr class="align-middle">
                            <th scope="col">Artículo</th>
                            <th scope="col">Personaje</th>
                            <th scope="col">Casa</th>
                            <th scope="col">Año de muerte</th>
                        </tr>
                    </thead>
                    <tbody class="table-group-divider">
                        <tr v-for="(item, index) in items" :key="index">
                            <td>
                                <NuxtLink :to="{ name: 'deaths-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-primary text-decoration-none">
                                    Muerte de {{ item.name }}
                                </NuxtLink>
                            </td>
                            <td>
                                <NuxtLink
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-primary text-decoration-none">
                                    {{ item.name }}
                                </NuxtLink>
                            </td>
                            <td>
                                <span v-if="!item.allegiances">Desconocidas</span>
                                <span v-else-if="item.allegiances === 'None'">Ninguna</span>
                                <NuxtLink v-else
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.allegiances) } }"
                                    class="text-primary text-decoration-none">
                                    {{ item.allegiances }}
                                </NuxtLink>
                            </td>
                            <td>{{ item.death_year ? item.death_year : 'Desconocido' }}</td>
                        </tr>
                    </tbody>
                    <tfoot class="table-group-divider">
                        <tr>
                            Cantidad total: {{ items.length }}
                        </tr>
                    </tfoot>
                </table>
            </div>
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const items = (await queryContent('/deaths').only('body').findOne()).body;
</script>