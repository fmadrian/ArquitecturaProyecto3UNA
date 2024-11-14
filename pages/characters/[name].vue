<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3" v-if="item">
                <h3> {{ item.alias ? `${item.alias}/` : '' }}{{ item.name }}</h3>
                <h4>Información general</h4>
                <table class="table table-responsive table-primary table-striped table-bordered">
                    <tbody>
                        <tr>
                            <td>Nombre de personaje</td>
                            <td>{{ item.name }}</td>
                        </tr>
                        <tr>
                            <td>Actor</td>
                            <td>{{ item.star }}</td>
                        </tr>
                        <tr>
                            <td>Episodios</td>
                            <td>{{ item.episodes_appeared }}</td>
                        </tr>
                        <tr>
                            <td>Primera aparición</td>
                            <td>{{ item.first_appearance }}</td>
                        </tr>
                        <tr>
                            <td>Última aparición</td>
                            <td>{{ item.last_appearance }}</td>
                        </tr>
                        <tr v-if="death">
                            <td>Muerte</td>
                            <td>
                                <NuxtLink :to="{ name: 'deaths-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-primary text-decoration-none">
                                    Muerte de {{ item.name }}
                                </NuxtLink>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <ArticleNotFound v-else itemType="Personaje" to="/characters" text="Personajes" />
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const route = useRoute()

const item = (await queryContent('/characters').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

const death = (await queryContent('/deaths').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())
</script>