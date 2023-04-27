<template>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">MY TODO LIST</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                </ul>
                <form class="d-flex" role="search" @submit.prevent="buscarNota">
                    <input class="form-control me-2" type="search" placeholder="Búsqueda" aria-label="Buscar" v-model="filtro">
                    <button class="btn btn-outline-success">Buscar</button>
                </form>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    data() {
        return {
            filtro : ''
        }
    },
    methods: {
        buscarNota(){
            this.$emit('buscarNota', this.filtro)
        }
    },
}
</script>