<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3" v-if="item">
                <h3>{{ item.name }} ({{ item.year }})</h3>
                <h4>Información general</h4>
                <table class="table table-responsive table-primary table-striped table-bordered">
                    <tbody>
                        <tr>
                            <td>Nombre</td>
                            <td>{{ item.name }}</td>
                        </tr>
                        <tr>
                            <td>Año</td>
                            <td>{{ item.year }}</td>
                        </tr>
                        <tr>
                            <td>Número de batalla</td>
                            <td>{{ item.battle_number }}</td>
                        </tr>
                        <tr>
                            <td>Región / Ubicación</td>
                            <td>
                                <NuxtLink
                                    :to="{ name: 'locations-name', params: { name: encodeURIComponent(item.region) } }"
                                    class="text-decoration-none">
                                    {{ item.region }}
                                </NuxtLink> / {{ item.location }}
                            </td>
                        </tr>
                        <tr v-if="item.notes && !item.notes !== ''">
                            <td>Notas</td>
                            <td>
                                {{ item.notes }}
                            </td>
                        </tr>
                        <tr>
                            <td>Resultado del atacante</td>
                            <td>{{ !item.attacker_outcome ? 'Desconocido' : item.attacker_outcome === 'win' ? 'Victoria'
                                + ' del atacante' : 'Victoria del defensor' }}</td>
                        </tr>
                        <tr>
                            <td>Tipo de batalla</td>
                            <td>{{ item.battle_type ? item.battle_type : 'Desconocido' }}</td>
                        </tr>
                        <tr>
                            <td>Verano</td>
                            <td>{{ item.summer === 1 ? 'Sí' : 'No' }}</td>
                        </tr>
                        <tr>
                            <td>Muertes importantes</td>
                            <td>{{ item.major_death === 1 ? 'Sí' : 'No' }}</td>
                        </tr>
                        <tr>
                            <td>Capturas importantes</td>
                            <td>{{ item.major_capture === 1 ? 'Sí' : 'No' }}</td>
                        </tr>

                    </tbody>
                </table>

                <!-- Atacante -->
                <h4>Atacante</h4>
                <table class="table table-responsive table-primary table-striped table-bordered">
                    <tbody>
                        <tr>
                            <td>Rey atacante</td>
                            <td>
                                <NuxtLink v-if="item.attacker_king"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.attacker_king) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_king }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr>
                            <td>Tamaño del atacante</td>
                            <td>{{ item.attacker_size ? item.attacker_size : 'Desconocido' }}</td>
                        </tr>
                        <tr>
                            <td>Comandante(s) del atacante</td>
                            <td>
                                <NuxtLink v-if="item.attacker_commander"
                                    v-for="(commander, index) in item.attacker_commander.trim().split(',')" :key="index"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(commander.trim()) } }"
                                    class="text-decoration-none">
                                    {{ commander }},
                                </NuxtLink>
                            </td>

                        </tr>
                        <tr v-if="item.attacker_1">
                            <td>Atacante 1</td>
                            <td>
                                <NuxtLink v-if="item.attacker_1"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.attacker_1) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_1 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.attacker_2">
                            <td>Atacante 2</td>
                            <td>
                                <NuxtLink v-if="item.attacker_2"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.attacker_2) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_2 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.attacker_3">
                            <td>Atacante 3</td>
                            <td>
                                <NuxtLink v-if="item.attacker_3"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.attacker_3) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_3 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.attacker_4">
                            <td>Atacante 4</td>
                            <td>
                                <NuxtLink v-if="item.attacker_4"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.attacker_4) } }"
                                    class="text-decoration-none">
                                    {{ item.attacker_4 }}
                                </NuxtLink>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <!-- Defensor -->
                <h4>Defensor</h4>
                <table class="table table-responsive table-primary table-striped table-bordered">
                    <tbody>
                        <tr>
                            <td>Rey defensor</td>
                            <td>
                                <NuxtLink v-if="item.defender_king"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.defender_king) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_king }}
                                </NuxtLink>
                                <span v-else>Desconocido</span>
                            </td>
                        </tr>
                        <tr>
                            <td>Tamaño del defensor</td>
                            <td>{{ item.defender_size ? item.defender_size : 'Desconocido' }}</td>
                        </tr>

                        <tr>
                            <td>Comandante(s) del defensor</td>
                            <td>
                                <NuxtLink v-if="item.defender_commander"
                                    v-for="(commander, index) in item.defender_commander.trim().split(',')" :key="index"
                                    :to="{ name: 'characters-name', params: { name: encodeURIComponent(commander.trim()) } }"
                                    class="text-decoration-none">
                                    {{ commander }},
                                </NuxtLink>
                                <span v-else>Desconocido</span>
                            </td>
                        </tr>
                        <tr v-if="item.defender_1">
                            <td>Defensor 1</td>
                            <td>
                                <NuxtLink v-if="item.defender_1"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.defender_1) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_1 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.defender_2">
                            <td>Defensor 2</td>
                            <td>
                                <NuxtLink v-if="item.defender_2"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.defender_2) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_2 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.defender_3">
                            <td>Defensor 3</td>
                            <td>
                                <NuxtLink v-if="item.defender_3"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.defender_3) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_3 }}
                                </NuxtLink>
                            </td>
                        </tr>
                        <tr v-if="item.defender_4">
                            <td>Defensor 4</td>
                            <td>
                                <NuxtLink v-if="item.defender_4"
                                    :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.defender_4) } }"
                                    class="text-decoration-none">
                                    {{ item.defender_4 }}
                                </NuxtLink>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <ArticleNotFound v-else itemType="Batalla" to="/battles" text="Batallas" />
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const route = useRoute()

const item = (await queryContent('/battles').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

</script>