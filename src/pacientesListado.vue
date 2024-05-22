<template>
  <div class="pacientesListado text-center">
    <div class="m-3" style="width: 18rem;">
      <div class="car-body px-3">
        <h5 class="card-title">Paciente</h5>
        <p class="card-text">{{ nombre }}</p>
        <h5 class="card-title">Fecha</h5>
        <p class="card-text">{{ fecha }}</p>
        <h5 class="card-title">Hora</h5>
        <p class="card-text">{{ hora }}</p>
        <h5 class="card-title">Motivo</h5>
        <p class="card-text">{{ motivo }}</p>
        <button class="btn btn-danger" @click="$emit('eliminarPaciente')">Eliminar Paciente</button>
      </div>
    </div>
  </div>
</template>


<script>


export default {
  name: 'pacientesListado',
  props: {
    nombre: String,
    fecha: String,
    hora: String,
    motivo: String,
    gravedad: String
  },


  components: {
  },
}
</script>

<style>
/* .card{
  background-color: transparent;
} */
</style>