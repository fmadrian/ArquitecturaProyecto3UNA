<template>
    <div class="container">
        <div class="d-flex flex-column row-gap-4">
            <HeaderView />

            <div class="d-flex flex-column row-gap-2">
                <h1>Proyecto 3</h1>
                <h3>Arquitectura de información</h3>
                <div class="d-flex flex-column">
                    <h5>Fernanda Quesada</h5>
                    <h5>Adrián Fallas</h5>
                </div>
            </div>

            <div class="d-flex flex-row column-gap-2 row-gap-4 align-items-center justify-content-around  flex-wrap">
                <MenuCard class="col-3" title="Casas"
                    src="https://images.vexels.com/content/78080/preview/game-of-thrones-houses-03e8d1.png"
                    to="/houses" />
                <MenuCard class="col-3" title="Batallas"
                    src="https://static1.colliderimages.com/wordpress/wp-content/uploads/2023/06/gotbattlemulti.jpg"
                    to="/battles" />
                <MenuCard class="col-3" title="Muertes" src="https://i.imgflip.com/4s4jwa.png?a480648" to="/deaths" />
                <MenuCard class="col-3" title="Ubicaciones"
                    src="https://www.expedia.com/stories/wp-content/uploads/2021/09/dragonstone-1.jpg"
                    to="/locations" />
                <MenuCard class="col-3" title="Personajes"
                    src="https://i0.wp.com/the-avocado.org/wp-content/uploads/2019/05/n.jpg" to="/characters" />
            </div>

            <FooterView />
        </div>
    </div>
</template>
<script setup>

</script>

<!--https://png.pngtree.com/background/20230519/original/pngtree-stairway-leading-up-to-heaven-in-the-clouds-picture-image_2665145.jpg-->