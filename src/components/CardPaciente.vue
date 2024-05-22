<template>
    <div id="cardPaciente">
        <div class="card" :class="cita.gravedad == 'Baja'?'text-bg-success' : cita.gravedad == 'Media' ? 'text-bg-warning' : cita.gravedad =='Alta' ?'text-bg-danger': ' ' ">
            <div class="card-body">
                <h6 class="card-title">Paciente</h6>
                <p class="card-text"> {{ cita.paciente }}</p>
                <h6 class="card-title">Fecha</h6>
                <p class="card-text"> {{ cita.fecha}}</p>
                <h6 class="card-title">Hora</h6>
                <p class="card-text">  {{ cita.hora }}</p>
                <h6 class="card-title">Motivo</h6>
                <p class="card-text">  {{ cita.motivo }}</p>
                <button class="btn btn-light" @click= "$emit('eliminar')">Eliminar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CardPaciente",
    props:{
        cita: Object,
    }
}
</script>

<style></style>