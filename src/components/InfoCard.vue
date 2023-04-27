<script>
import NewTodo from './Modals/NewTodo.vue';

export default {
    props: {
        texto: {
            type: String
        },
        boton: {
            type: String,
            default: null
        }
    },
    components: { NewTodo }
}
</script>

<template>
  <section class="tarjeta-texto">
    <div class="parrafo-info">
        <p>{{ texto }}</p>
        <NewTodo v-if="boton" :textoBoton="boton" @nueva-nota="$emit('nueva-nota')"/>
    </div>
  </section>
</template>