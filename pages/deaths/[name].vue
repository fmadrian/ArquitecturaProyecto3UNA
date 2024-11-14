<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="d-flex flex-column row-gap-3" v-if="item">
            <h3>Muerte de {{ item.name }} {{ item.death_year ? `(${item.death_year})` : '' }}</h3>
            <h4>Información general</h4>
            <table class="table table-responsive table-primary table-striped table-bordered">
                <tbody>
                    <tr>
                        <td>Nombre</td>
                        <td>
                            <NuxtLink v-if="character"
                                :to="{ name: 'characters-name', params: { name: encodeURIComponent(item.name) } }"
                                class="text-primary text-decoration-none">
                                {{ item.name }}
                            </NuxtLink>
                            <span v-else>{{ item.name }}</span>
                        </td>
                    </tr>
                    <tr>
                        <td>Año de muerte</td>
                        <td>{{ item.death_year ? item.death_year : 'Desconocido' }}</td>
                    </tr>
                    <tr>
                        <td>Libro de muerte</td>
                        <td>
                            {{ item.book_of_death ? item.book_of_death : 'Desconocido' }}
                        </td>
                    </tr>
                    <tr v-if="item.notes && !item.notes !== ''">
                        <td>Capítulo de muerte</td>
                        <td>
                            {{ item.death_chapter ? item.death_chapter : 'Desconocido' }}
                        </td>
                    </tr>
                    <tr>
                        <td>Capítulo de introducción de libro</td>
                        <td>
                            {{ item.book_intro_chapter ? item.book_intro_chapter : 'Desconocido' }}
                        </td>
                    </tr>
                    <tr>
                        <td>Género</td>
                        <td>{{ item.gender === 1 ? 'Hombre' : 'Mujer' }}</td>
                    </tr>
                    <tr>
                        <td>¿Era noble?</td>
                        <td>{{ item.summer === 1 ? 'Sí' : 'No' }}</td>
                    </tr>
                </tbody>
            </table>
            <h4>Apariciones en libros</h4>
            <table class="table table-responsive table-secondary table-striped table-bordered">
                <thead>
                    <tr>
                        <th scope="col">Primer libro</th>
                        <th scope="col">Segundo libro</th>
                        <th scope="col">Tercer libro</th>
                        <th scope="col">Cuarto libro</th>
                        <th scope="col">Quinto libro</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td :class="item.GoT === 1 ? 'table-success' : 'table-danger'">{{ item.GoT === 1 ? 'Sí' : 'No'
                            }}</td>
                        <td :class="item.CoK === 1 ? 'table-success' : 'table-danger'">{{ item.CoK === 1 ? 'Sí' : 'No'
                            }}</td>
                        <td :class="item.SoS === 1 ? 'table-success' : 'table-danger'">{{ item.SoS === 1 ? 'Sí' : 'No'
                            }}</td>
                        <td :class="item.FfC === 1 ? 'table-success' : 'table-danger'">{{ item.FfC === 1 ? 'Sí' : 'No'
                            }}</td>
                        <td :class="item.DwD === 1 ? 'table-success' : 'table-danger'">{{ item.DwD === 1 ? 'Sí' : 'No'
                            }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <ArticleNotFound v-else itemType="Muerte" to="/deaths" text="Muertes" />
        <FooterView />
    </div>
</template>
<script setup>
const route = useRoute()

const item = (await queryContent('/deaths').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

const character = (await queryContent('/characters').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())
</script>