<template>
  <div id="app" class="container text-center py-3">
    <main>
      <h1 class=py-2>Citas médicas</h1>
      <!-- El punto prevent es para que no se recargue la página. -->
      <form class="border rounded p-3" @submit.prevent="agregarCita">
        <!-- d-md-flex para que haga flex desde pantallas medianas en adelante y el flex wrap para que lo haga desde las medianas a las grandes -->
        <div class="d-md-flex flex-wrap justify-content-around">
          <!--PACIENTES-->
          <div>
            <!-- Hicimos un biding de la clase, que dice si esque no hay nada en cita.paciente ? (entonces) texte danger : (else) dejame el string ' ' text--->
            <label for="" class="form-label" :class="!cita.pacientes ? 'text-danger' : ' '">Paciente: </label>
            <input type="text" class="form-control" v-model="cita.pacientes" />
          </div>
          <!--FECHA-->
          <div>
            <label for="" class="form-label" :class="!cita.fecha ? 'text-danger' : ' '">Fecha: </label>
            <input type="date" class="form-control" v-model="cita.fecha" />
          </div>
          <!--HORA-->
          <div>
            <label for="" class="form-label" :class="!cita.hora ? 'text-danger' : ' '">Hora: </label>
            <input type="time" class="form-control" v-model="cita.hora" />
          </div>
          <!--GRAVEDAD-->
          <div>
            <label for="" class="form-label" :class="!cita.gravedad ? 'text-danger' : ' '">Gravedad: </label>
            <select class="form-select" name="graveades" id="gravedades" v-model="cita.gravedad">
              <option :value="gravedad" v-for="(gravedad, index) in gravedades" :key="index"> {{ gravedad }}</option>
            </select>
          </div>
          <!--MOTIVO-->
          <div>
            <label for="" class="form-label" :class="!cita.motivo ? 'text-danger' : ' '">Motivo: </label>
            <input type="text" class="form-control" v-model="cita.motivo" />
          </div>
        </div>
        <!-- BOTON -->
        <div class=py-4>
          <!-- || significa ó -->
          <button type="submit" class="btn btn-light"
            :disabled="!cita.pacientes || !cita.fecha || !cita.hora || !cita.gravedad || !cita.motivo">Agregar</button>
        </div>
      </form>
      <div>
        <p class="text-danger" v-if="citas.length < 1"> Aún no hay consultas registradas</p>
        <div v-else class="row g-2">
          <div class="col-12 col-md-6 col-lg-4 py-4" v-for="(cita, index) in citas" :key="index">
            <!-- El :cita es el nombre del props que le di en CardPaciente y el ="cita" es lo que le voy a pasar que esta en app.vue -->
            <CardPaciente :cita="cita" @eliminar="eliminarHandler(index)"/>
          </div>
        </div>
      </div>

    </main>
  </div>
</template>

<script>
import CardPaciente from "./components/CardPaciente.vue"
export default {
  name: "App",
  components: {
    CardPaciente,
  },
  data() {
    return {
      citas: [],
      cita: {
        pacientes: "",
        fecha: "",
        hora: "",
        gravedad: "",
        motivo: "",
      },

      gravedades: [
        "Baja", "Media", "Alta",
      ],

      motivo: "",

    };
  },
  //es una función a un array un objeto.
  methods: {
    agregarCita() {
      this.citas.push(this.cita);
      this.cita = {};
    },
    eliminarHandler(index){
     if(confirm ('¿Estás seguro que deseas eliminar esta cita?')){this.citas.splice(index,1)
     } 
    },
  },
  computed: {},
};
</script>

<style></style>