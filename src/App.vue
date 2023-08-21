<script setup>
import { ref, reactive } from "vue";

import { uid } from "uid";

import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";

const pacientes = ref([]);

const paciente = reactive({
  id: null,
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintoma: "",
});

const guardarPaciente = () => {
  if (paciente.id) {
    const { id } = paciente;
    const indice = pacientes.value.findIndex((pacienteState) => {
      pacienteState.id === id;
    });
    pacientes.value[indice] = { ...paciente };
  } else {
    pacientes.value.push({ ...paciente, id: uid() });
  }

  Object.assign(paciente, {
    nombre: "",
    propietario: "",
    email: "",
    alta: "",
    sintoma: "",
    id: null,
  });
};

const actualizarPaciente = (idPaciente) => {
  const pacienteEditar = pacientes.value.filter((paciente) => {
    return paciente.id === idPaciente;
  })[0];
  console.log(pacienteEditar);
  Object.assign(paciente, pacienteEditar);
};

const eliminarPaciente = (idPaciente) => {
  const pacienteEditar = pacientes.value.filter((paciente) => {
    return paciente.id === idPaciente;
  })[0];

  //Para eliminar elemento del arreglo paciente
  pacientes.value.splice(
    pacientes.value.findIndex((paciente) => {
      return paciente.id === pacienteEditar.id;
    }),
    1
  );
};
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintoma="paciente.sintoma"
        @guardar-paciente="guardarPaciente"
      />
      <div class="overflow-y-scroll md:w-1/2 md:h-screen">
        <h3 class="text-3xl font-black text-center">
          Administra tus pacientes
        </h3>

        <div v-if="pacientes.length > 0">
          <Paciente
            v-for="(paciente, i) in pacientes"
            :key="i"
            :paciente="paciente"
            @actualizar-paciente="actualizarPaciente"
            @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>

