<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3" v-if="item">
                <h3> {{ item.name }}</h3>
                <h4>Regiones</h4>
                <table class="table table-responsive table-primary table-striped table-bordered"
                    v-if="item.regions.length > 0">
                    <thead>
                        <tr>
                            <th scope="col">Nombre</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(region, index) in item.regions" :key="index">
                            <td>
                                <NuxtLink :to="{ name: 'locations-name', params: { name: encodeURIComponent(region) } }"
                                    class="text-decoration-none">
                                    {{ region }}
                                </NuxtLink>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <span class="d-inline fs-6" v-else>
                    No hay regiones.
                </span>
                <h4>Miembros</h4>
                <table class="table table-responsive table-primary table-striped table-bordered"
                    v-if="item.characters.length > 0">
                    <table class="table table-responsive table-primary table-striped table-bordered">
                        <thead>
                            <tr>
                                <th scope="col">Nombre</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(character, index) in item.characters" :key="index">
                                <td>
                                    <NuxtLink
                                        :to="{ name: 'characters-name', params: { name: encodeURIComponent(character) } }"
                                        class="text-decoration-none">
                                        {{ character }}
                                    </NuxtLink>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </table>
                <span class="d-inline fs-6" v-else>
                    No hay regiones.
                </span>
                <PrevNext :prev="prev" :next="next" basePath="houses" />
            </div>
            <ArticleNotFound v-else itemType="Casa" to="/houses" text="Casas" />
        </div>
        <FooterView />
    </div>
</template>
<script setup>
import PrevNext from '~/components/PrevNext.vue'
const route = useRoute()

const items = (await queryContent('/houses').only('body').findOne()).body
const item = items.find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

const currentIndex = items.indexOf(item)
const prev = currentIndex > 0 ? items[currentIndex - 1] : null
const next = currentIndex < items.length - 1 ? items[currentIndex + 1] : null        
</script>