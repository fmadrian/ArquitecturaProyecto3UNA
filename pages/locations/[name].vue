<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3" v-if="item">
                <h3> {{ item.name }}</h3>
                <img v-if="item.img" :src="item.img" :alt="'Imagen de ' + item.name"  class="max-size"/>
                <h4>Subregiones</h4>
                <table class="table table-responsive table-primary table-striped table-bordered"
                    v-if="item.sublocations.length > 0">
                    <thead>
                        <tr>
                            <th scope="col">Nombre</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(subregion, index) in item.sublocations" :key="index">
                            <td>{{ subregion }} </td>
                        </tr>
                    </tbody>
                </table>
                <span class="fs-6" v-else>No hay subregiones</span>
                <PrevNext :prev="prev" :next="next" basePath="locations" />
            </div>
            <ArticleNotFound v-else itemType="Región" to="/locations" text="Regiones" />
        </div>
        <FooterView />
    </div>
</template>
<script setup>
import PrevNext from '~/components/PrevNext.vue'
const route = useRoute()

const items = (await queryContent('/locations').only('body').findOne()).body
const item = items.find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

const currentIndex = items.indexOf(item)
const prev = currentIndex > 0 ? items[currentIndex - 1] : null
const next = currentIndex < items.length - 1 ? items[currentIndex + 1] : null   
</script>
<style scoped>
.max-size {
  max-width: 300px;
  max-height: 200px;
  object-fit: contain;
}
</style>