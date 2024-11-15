<!-- pages/authors_index.vue -->
<template>
    <div class="container">
        <HeaderView />
        <div class="row py-3">
            <div class="d-flex flex-column row-gap-3">
                <h3>Casas</h3>
                <input
                    v-model="searchQuery"
                    type="text"
                    placeholder="Buscar Casas..."
                    class="form-control mb-3"
                />
                <table class="table table-responsive table-primary table-striped table-sm align-middle table-bordered">
                    <thead>
                        <tr class="align-middle">
                            <th scope="col">Nombre</th>
                        </tr>
                    </thead>
                    <tbody class="table-group-divider">
                        <tr v-for="(item, index) in filteredItems" :key="index">
                            <td>
                                <NuxtLink :to="{ name: 'houses-name', params: { name: encodeURIComponent(item.name) } }"
                                    class="text-decoration-none">
                                    {{ item.name }}
                                </NuxtLink>
                            </td>
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
const items = (await queryContent('/houses').only('body').findOne()).body;
// Barra de búsqueda
const searchQuery = ref('');

//Filtro de búsqueda
const filteredItems = computed(() => {
    return items.filter(item =>
        item.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    );
});
</script>