<script>

export default {
    props: {
        nota: {
            type: Object
        },
    },
    methods: {
        actualizarColor(color){
            let notasLS = JSON.parse(localStorage.getItem('notas'));
            let nota = notasLS.find(nota => nota.titulo === this.nota.titulo);

            nota.color = color;
            
            localStorage.setItem('notas', JSON.stringify(notasLS));
            this.$emit('colorCambiado');
        }
    },
    computed : {
        colorTarjeta() {
            if(!this.nota.color || this.nota.color == 'verde'){
                return 'tarjeta-verde'
            }else if(this.nota.color == 'morado'){
                return 'tarjeta-morada'   
            }else if(this.nota.color == 'rojo'){
                return 'tarjeta-roja'   
            }else if(this.nota.color == 'amarillo'){
                return 'tarjeta-amarilla'   
            }
        }
    }
}
</script>

<template>
    <section :class="`tarjeta-nota ${colorTarjeta}`">
        <h2>{{ nota.titulo }}</h2>
        <p>{{ nota.descripcion }}</p>
        <button class="btn btn-primary dropdown-toggle btn-sm" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
            Color
        </button>
        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
            <li @click="actualizarColor('verde')"><a class="dropdown-item" href="#">Verde</a></li>
            <li @click="actualizarColor('morado')"><a class="dropdown-item" href="#">Morado</a></li>
            <li @click="actualizarColor('rojo')"><a class="dropdown-item" href="#">Rojo</a></li>
            <li @click="actualizarColor('amarillo')"><a class="dropdown-item" href="#">Amarillo</a></li>
        </ul>
        <button class="btn btn-danger btn-sm" type="button">Eliminar nota</button>
    </section>
</template>