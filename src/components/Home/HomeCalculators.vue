<template>
    <div class="q-pa-md">
      <div class="row q-gutter-md justify-center">
        <!-- Gerando os cards dinamicamente -->
        <q-card
        v-for="(calculator, index) in calculators"
        :key="index"
        class="col-12 col-sm-6 col-md-4 col-lg-3"
        flat
        bordered
        >
          <q-card-section>
            <!-- Nome da calculadora -->
            <div class="text-h6 text-primary">{{ calculator.name }}</div>
            <!-- Descrição -->
            <p class="text-body2 q-mt-sm">{{ calculator.description }}</p>
          </q-card-section>
          <q-separator />
          <!-- Link para a página -->
          <q-card-actions align="right">
            <q-btn
              :label="'Acessar'"
              tag="router-link"
              :to="calculator.link"
              color="primary"
              flat
            />
          </q-card-actions>
        </q-card>
      </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

const calculators = ref([
  {
    name: "Calculadora de Incertezas",
    description: "Realiza cálculos de incertezas, com base em uma lista de valores.",
    link: "/calculators/uncertainties",
  },
]);
</script>

<style scoped>
/* Ajuste de estilo para os cards */
.q-card {
  transition: transform 0.3s;
}
.q-card:hover {
  transform: scale(1.05);
}
</style>
