<template>
  <div class="q-ma-lg">
    <div class="q-gutter-md row flex-center">
      <q-input
        v-model="measures"
        label="Medidas"
        class="col-12 col-sm"
        outlined
      />
      <q-input
        v-model="uncertaintiesB"
        label="Incerteza B"
        class="col-12 col-sm"
        outlined
      />

      <q-btn
        label="CALCULAR"
        @click="fetchData"
        class="col-12 col-md-12"
        size="lg"
      />
    </div>
  </div>
</template>


<script setup>
import { ref } from "vue";

const measures = ref("");
const uncertaintiesB = ref("");

const emit = defineEmits(['setCalculatedData']);

// const apiBaseUrl = import.meta.env.VITE_API_BASE_URL;
const apiBaseUrl = process.env.API_BACKEND_URL;

const fetchData = async () => {
  try {
    const response = await fetch(`${apiBaseUrl}/uncertainties`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        measures: measures.value,
      }),
    });

    if (!response.ok) {
      throw new Error('Erro ao fazer a requisição');
    }

    const data = await response.json();
    console.log(data)

    // Emitir os dados para o componente pai
    emit('setCalculatedData', data);
  } catch (error) {
    console.error('Erro ao realizar a requisição:', error);
  }
};
</script>