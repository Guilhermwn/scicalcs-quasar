<template>
    <q-page class="page">
        <UncertaintiesMeasures @setCalculatedData="updateCalculatedData"/>
        <q-separator spaced inset />
        <UncertaintiesCalculated :calculatedData="calculatedData"/>
    </q-page>
</template>

<script setup>
import UncertaintiesMeasures from "components/Calculators/Uncertainties/UncertaintiesMeasures.vue"
import UncertaintiesCalculated from "components/Calculators/Uncertainties/UncertaintiesCalculated.vue"
import { ref } from "vue";

const calculatedData = ref(null)

const updateCalculatedData = (data) => {
    calculatedData.value = data;
}
</script>

<style scoped>
.page {
  margin-right: 15px;
  padding-inline: 2em 2em;
}
</style>