<script>
import InfoCard from '../components/InfoCard.vue'
import TitleCard from '../components/TitleCard.vue'
import Navbar from './../components/Navbar.vue'
import axios from 'axios';
import NoteCard from '../components/NoteCard.vue';

export default {
  data() {
    return {
      temperatura: '0',
      notas : JSON.parse(localStorage.getItem('notas')),
      filtro : ''
    }
  },
  computed: {
    textoTemperatura() {
      return `Temperatura actual: ${this.temperatura}°c`;
    },
  },
  components: {
    Navbar,
    TitleCard,
    InfoCard,
    NoteCard
  },
  async mounted() {
    // this.temperatura = await this.obtenerTemperatura();
  },
  methods: {
    obtenerTemperatura() {
      return new Promise((res, rej) => {
        if (navigator.geolocation) {
          var success = async function (position) {
            var latitud = position.coords.latitude,
              longitud = position.coords.longitude;

            const { data } = await axios.get(`http://dataservice.accuweather.com/locations/v1/cities/geoposition/search?apikey=FLvIV5CHKgXjvkaA4vKIb2GDASZnEGZK&q=${latitud},${longitud}`);
            const key = data.Key ? data.Key : null;

            if (key) {
              const req = await axios.get(`http://dataservice.accuweather.com/currentconditions/v1/${key}?apikey=FLvIV5CHKgXjvkaA4vKIb2GDASZnEGZK&language=es-mx`);
              res(req.data[0].Temperature ? req.data[0].Temperature.Metric.Value : '-');
            }
          }
          navigator.geolocation.getCurrentPosition(success, function (msg) {
            console.error(msg)
            rej('-');
          });
        } else {
          rej('-')
        }

      })
    },
    actualizarNotas(){
      this.notas = JSON.parse(localStorage.getItem('notas'));
    },
    buscar(filtro){
      this.filtro = filtro;
    }
  },
}
</script>

<template>
  <div>
    <header>
      <Navbar @buscarNota="buscar"/>
    </header>
    <main class="principal">
      <article>
        <title-card titulo="Bienvenido"
          texto="Este espacio es para que generes tus listas de pendientes, es un espacio cómodo y gratuito para tu servicio. El proyecto está realizado con las siguientes características:"
          :lista="[
            'VueJS 3',
            'HTML',
            'CSS con diseño responsivo, flexbox y css grid.',
            'Github',
            'Eventos y arreglos',
            'Actualización del DOM',
            'Promesas asíncronas',
            'Uso de local storage'
          ]" />
        <info-card :texto="textoTemperatura" boton="Nueva nota" @nueva-nota="actualizarNotas"/>
      </article>
      <article class="notas" v-if="notas">
        <template v-for="nota, index in notas" :key="index">
          <note-card v-if="filtro == '' || nota.titulo.includes(filtro) || nota.descripcion.includes(filtro)" :nota="nota" @colorCambiado="actualizarNotas" @notaEliminada="actualizarNotas"/>
        </template>
      </article>
    </main>
  </div>
</template>
