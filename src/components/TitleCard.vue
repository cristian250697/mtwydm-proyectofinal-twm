<script>
export default {
    props: {
        titulo: {
            type: String
        },
        texto: {
            type: String
        },
        lista: {
            type: Array,
            default: []
        }
    }
}
</script>

<template>
    <section class="tarjeta-texto">
        <h1 class="titulo" v-if="titulo">{{ titulo }}</h1>
        <div class="parrafo">
            <p>{{ texto }}</p>
            <template v-if="lista.length > 0">
                <ul>
                    <li v-for="elemento, index in lista" :key="index">{{ elemento }}</li>
                </ul>
            </template>
        </div>
    </section>
</template>