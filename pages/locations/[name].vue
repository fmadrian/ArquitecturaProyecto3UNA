<!-- pages/director/[...id].vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3">

                <h3> {{ item.name }}</h3>
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
            </div>
        </div>
        <FooterView />
    </div>
</template>
<script setup>
const route = useRoute()

const item = (await queryContent('/locations').only('body').findOne()).body
    .find(item => item.name.trim() === decodeURIComponent(route.params.name).trim())

</script>