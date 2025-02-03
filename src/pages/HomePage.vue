<template>
  <q-page class="page">
    <HomeHeader />
    <HomeCalculators />
  </q-page>
</template>

<script setup>
import HomeHeader from "components/Home/HomeHeader.vue"
import HomeCalculators from "components/Home/HomeCalculators.vue"
</script>

<style scoped>
.page {
  margin: 20px;
}

.my-card{
  width: 100%;
  max-width: 250px;
}
</style>