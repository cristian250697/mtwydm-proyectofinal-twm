<script>

export default {
    props: {
        titulo: {
            type: String
        },
        descripcion: {
            type: String,
        }
    }
}
</script>

<template>
    <section class="tarjeta-nota">
        <h2>{{ titulo }}</h2>
        <p>{{ descripcion }}</p>
    </section>
</template>