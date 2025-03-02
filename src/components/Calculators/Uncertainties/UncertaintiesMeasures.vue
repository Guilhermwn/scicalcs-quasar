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
import { useQuasar } from 'quasar'

const $q = useQuasar()

const measures = ref("");
const uncertaintiesB = ref("");

const emit = defineEmits(['setCalculatedData']);

const apiBaseUrl = import.meta.env.VITE_API_BACKEND_URL;
// const apiBaseUrl = "http://192.168.1.4:8000";
// const apiBaseUrl = process.env.API_BACKEND_URL;


const fetchData = async () => {
  try {
    $q.notify('Calculando...')
    const response = await fetch(`${apiBaseUrl}/uncertainties`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        measures: measures.value,
        uncertaintiesB: uncertaintiesB.value
      }),
    });

    if (!response.ok) {
      $q.notify('Erro ao fazer a requisição')
      throw new Error('Erro ao fazer a requisição');
    }

    const data = await response.json();
    console.log(data)

    // Emitir os dados para o componente pai
    emit('setCalculatedData', data);
  } catch (error) {
    $q.notify(`Erro ao realizar a requisição: ${error}`)
    console.error('Erro ao realizar a requisição:', error);
  }
};
</script>