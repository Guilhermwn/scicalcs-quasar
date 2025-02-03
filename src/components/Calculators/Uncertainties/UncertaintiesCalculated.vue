<template>
    <div v-if="calculatedData" class="q-ma-lg">
      <h2 class="text-h6 text-center">INCERTEZAS CALCULADAS</h2>
      <div class="row q-gutter-md justify-center">
        <q-card class="col-12 col-sm-4 col-md-3" @click="copy(`${calculatedData.mean}`)">
          <q-card-section>
            <div class="text-h6">Média</div>
            <div class="text-subtitle2">{{ calculatedData.mean }}</div>
          </q-card-section>
        </q-card>
        <q-card class="col-12 col-sm-4 col-md-3" @click="copy(`${calculatedData.stdDev}`)">
          <q-card-section>
            <div class="text-h6">Desvio Padrão</div>
            <div class="text-subtitle2">{{ calculatedData.stdDev }}</div>
          </q-card-section>
        </q-card>
        <q-card class="col-12 col-sm-4 col-md-3" @click="copy(`${calculatedData.uncertaintyA}`)">
          <q-card-section>
            <div class="text-h6">Incerteza A</div>
            <div class="text-subtitle2">{{ calculatedData.uncertaintyA }}</div>
          </q-card-section>
        </q-card>
      </div>  
    </div>
</template>
  
<script setup>
import { useQuasar } from 'quasar'
import { copyToClipboard } from 'quasar'


const $q = useQuasar()

const props = defineProps({
  calculatedData: {
    type: Object,
    default: () => null
  }
});

const copy = (text) => {
  copyToClipboard(text)
  .then(() => {
    $q.notify(`Copiado: ${text}`)
  })
  .catch(() => {
    // fail
  })
};1
</script>