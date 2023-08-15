<script setup>
import { ref } from "vue";
import Formulario from "./components/Formulario.vue";
import Header from "./components/Header.vue";

const pacientes = ref([]);
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />
    <div class="mt-12 md:flex">
      <Formulario />
      <div class="overflow-y-scroll md:w-1/2 md:h-screen">
        <h3 class="text-3xl font-black text-center">
          Administra tus pacientes
        </h3>

        <div v-if="pacientes.length > 0"></div>
        <p v-else class="mt-10 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>

