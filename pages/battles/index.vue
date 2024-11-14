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
                            <th scope="col">Número de batalla</th>
                            <th scope="col">Nombre</th>
                            <th scope="col">Año</th>

                            <th scope="col">Ubicación</th>
                            <th scope="col">Rey atacante</th>
                            <th scope="col">Rey defensor</th>
                            <th scope="col">Ganador</th>
                            <th scope="col">Tipo de batalla</th>
                        </tr>
                    </thead>
                    <tbody class="table-group-divider">
                        <tr v-for="(item, index) in items" :key="index">
                            <td>{{ item.battle_number ? item.battle_number : 'Desconocido' }}</td>
                            <td>
                                <NuxtLink
                                    :to="{ name: 'battles-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-primary text-decoration-none">
                                    {{ item.name }}
                                </NuxtLink>
                            </td>
                            <td>{{ item.year ? item.year : 'Desconocido' }}</td>
                            <td>
                                <NuxtLink v-if="item.location"
                                    :to="{ name: 'locations-name', params: { name: encodeURIComponent(item.location) } }"
                                    class="text-decoration-none">
                                    {{ item.location }}
                                </NuxtLink>
                                <span v-else>Desconocido</span>
                            </td>
                            <td>
                                <NuxtLink v-if="item.attacker_king"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.attacker_king) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_king }}
                                </NuxtLink>
                                <span v-else>Desconocido</span>
                            </td>
                            <td>
                                <NuxtLink v-if="item.defender_king"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.defender_king) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_king }}
                                </NuxtLink>
                                <span v-else>Desconocido</span>
                            </td>
                            <td>{{ !item.attacker_outcome ? 'Desconocido' : item.attacker_outcome === 'win' ? 'Atacante'
                                : 'Defensor' }}</td>
                            <td>{{ item.battle_type ? item.battle_type : 'Desconocido' }}</td>
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
const items = (await queryContent('/battles').only('body').findOne()).body;
</script>