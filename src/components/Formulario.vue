<script setup>
import { reactive, defineEmits, defineProps } from "vue";
import Alerta from "./Alerta.vue";

const alerta = reactive({
  tipo: "",
  mensaje: "",
});

const emit = defineEmits([
  "update:nombre",
  "update:propietario",
  "update:email",
  "update:alta",
  "update:sintoma",
  "guardar-paciente",
]);

const props = defineProps({
  nombre: {
    type: String,
    required: true,
  },
  propietario: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  alta: {
    type: String,
    required: true,
  },
  sintoma: {
    type: String,
    required: true,
  },
});

const validar = () => {
  if (Object.values(props).includes("")) {
    alerta.mensaje = "Todos los campos deben ser llenados.";
    alerta.tipo = "error";
    return;
  } else {
    alerta.mensaje = "Guardado correctamente.";
    alerta.tipo = "save";
    emit("guardar-paciente");

    setTimeout(() => {
      Object.assign(alerta, {
        tipo: "",
        mensaje: "",
      });
    }, 3000);
  }
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="text-3xl font-black text-center">Seguimiento Pacientes</h2>
    <p class="mt-5 mb-10 text-lg text-center">
      Añade Pacientes y
      <span class="font-bold text-indigo-600">Admínistralos</span>
    </p>
    <Alerta v-if="alerta.mensaje" :alerta="alerta" />
    <form
      class="px-5 py-10 mb-10 bg-white rounded-lg shadow-md"
      action=""
      @submit.prevent="validar"
    >
      <div class="mb-5">
        <label for="mascota" class="block font-bold text-gray-700 uppercase">
          Nombre Mascota
        </label>
        <input
          type="text"
          id="mascota"
          placeholder="Nombre de la mascota"
          class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label
          for="propietario"
          class="block font-bold text-gray-700 uppercase"
        >
          Nombre Dueño
        </label>
        <input
          type="text"
          id="propietario"
          placeholder="Nombre del propietario"
          class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
          :value="propietario"
          @input="$emit('update:propietario', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block font-bold text-gray-700 uppercase">
          Correo electronico
        </label>
        <input
          type="email"
          id="email"
          placeholder="Correo electronico"
          class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
          :value="email"
          @input="$emit('update:email', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="alta" class="block font-bold text-gray-700 uppercase">
          Alta
        </label>
        <input
          type="date"
          id="alta"
          placeholder="Alta de la mascota"
          class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
          :value="alta"
          @input="$emit('update:alta', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="sintoma" class="block font-bold text-gray-700 uppercase">
          Síntomas
        </label>
        <textarea
          id="sintoma"
          placeholder="Mencione los síntomas "
          class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
          :value="sintoma"
          @input="$emit('update:sintoma', $event.target.value)"
        />
      </div>

      <input
        type="submit"
        value="Registrar pacientes"
        class="w-full p-3 font-bold text-white uppercase transition-colors bg-indigo-600 cursor-pointer hover:bg-indigo-700"
      />
    </form>
  </div>
</template>

