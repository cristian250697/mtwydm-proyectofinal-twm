
<script>
export default {
    data() {
        return {
            titulo : '',
            descripcion : ''
        }
    },
    props: {
        textoBoton: {
            type: String
        }
    },
    methods : {
        cerrarModal() {
            this.titulo = '';
            this.descripcion = '';
            document.getElementById('close').click();
        },
        agregarNota() {
            const nuevaNota = {
                titulo : this.titulo,
                descripcion : this.descripcion,
                favorita : false
            };

            if(localStorage.getItem('notas') != null){

                let notas = JSON.parse(localStorage.getItem('notas'));
                notas.push(nuevaNota);

                localStorage.setItem('notas', JSON.stringify(notas));
            }else{
                localStorage.setItem('notas', JSON.stringify([nuevaNota]));
            }

            this.cerrarModal();
            this.$emit('nueva-nota')
        }
    }
}
</script>

<template>
    <div>
        <!-- Button trigger modal -->
        <button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#newToDoModal">
            {{ textoBoton }}
        </button>

        <!-- Modal -->
        <div class="modal fade" id="newToDoModal" tabindex="-1" aria-labelledby="newToDoModalLabel" data-bs-backdrop="static" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="newToDoModalLabel">Nueva nota</h5>
                        <button id="close" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Titulo</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" v-model="titulo">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlTextarea1" class="form-label">Descripción</label>
                            <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" v-model="descripcion"></textarea>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" @click="cerrarModal">Cancelar</button>
                        <button type="button" class="btn btn-success" @click="agregarNota">Guardar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>