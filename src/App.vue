<template>
  <div id="app">
    <section class="container mt-5">
      <form @submit.prevent="agregarPaciente">
        <div>
          <div class="row">
            <div class="col-3">
              <label for="paciente" class="form-label" :class="{ noactivo: !datosPaciente.nombre }">Paciente</label>
              <input type="text" class="form-control" id="paciente" v-model="datosPaciente.nombre">
            </div>
            <div class="col-2">
              <label for="fecha" class="form-label" :class="{ noactivo: !datosPaciente.fecha }">Fecha</label>
              <input type="date" class="form-control" id="fecha" v-model="datosPaciente.fecha">
            </div>
            <div class="col-2">
              <label for="hora" class="form-label" :class="{ noactivo: !datosPaciente.hora }">Hora</label>
              <input type="time" class="form-control" id="hora" v-model="datosPaciente.hora">
            </div>
            <div class="col-2">
              <label for="gravedad" class="form-label">Gravedad</label>
              <select class="form-select" aria-label="Default select example" v-model="datosPaciente.gravedad">
                <option v-for="(gravedad, index) in tiposGravedad" :key="index">{{ gravedad }}</option>
              </select>
            </div>
            <div class="col-3">
              <label for="motivo" class="form-label" :class="{ noactivo: !datosPaciente.motivo }">Motivo</label>
              <input type="text" class="form-control" id="motivo" v-model="datosPaciente.motivo">
            </div>
          </div>
        </div>
        <div class="mt-3 text-center">
          <button class="btn btn-secondary" @click="agregarPaciente" :disabled="!botonActivo">Agregar</button>
        </div>
      </form>
    </section>
    <section class="container d-flex my-4 gap-3 py-4">
      <pacientesListado v-for="(paciente, index) in listaPacientes" :key="index"
      :style="colorGravedad(paciente.gravedad)"
      :nombre="paciente.nombre"
      :fecha="paciente.fecha"
      :hora="paciente.hora"
      :motivo="paciente.motivo"
      @eliminarPaciente="listaPacientes.splice(index,1)"
      />
    </section>
    
  </div>
</template>

<script>
import PacientesListado from './components/pacientesListado.vue';

export default {
  name: 'App',
  components: {
    PacientesListado
  },
  data() {
    return {
      tiposGravedad: ['Baja', 'Media', 'Alta'],
      datosPaciente: {
        nombre: "",
        fecha: "",
        hora: "",
        motivo: "",
        gravedad: "",
      },
      listaPacientes: [
      {nombre: "Alejandra Pérez",
        fecha: "23/05/2024",
        hora: "10:00",
        motivo: "Tos leve",
        gravedad: "Baja",},
        {nombre: "Pedro Orellana",
        fecha: "24/05/2024",
        hora: "11:00",
        motivo: "Amigdalitis",
        gravedad: "Media",},
        {nombre: "Lourdes Arco",
        fecha: "22/05/2024",
        hora: "16:00",
        motivo: "Traumatismos",
        gravedad: "Alta",}
      ],
    }
  },
  methods: {
    agregarPaciente: function () {
      const nuevoPaciente = Object.assign({}, this.datosPaciente);
      this.listaPacientes.push(nuevoPaciente);
      this.datosPaciente = { nombre: '', fecha: '', hora: '', motivo: '' }
    },
    colorGravedad: function(gravedad){
    if (gravedad === 'Baja'){
      return 'background-color: #95dc82;'
    }else if (gravedad === 'Media'){
      return 'background-color: #e7e579;'
    }else if (gravedad === 'Alta'){
      return 'background-color: #92524b;'
    }
    }
  },
  computed: {
  botonActivo: function () {
      return this.datosPaciente.nombre && this.datosPaciente.fecha && this.datosPaciente.hora && this.datosPaciente.gravedad && this.datosPaciente.motivo
    }
  }
}
</script>

<style>
.noactivo {
  color: red;
}
</style>
