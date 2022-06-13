<script setup>
import Form from './components/Form.vue'
</script>

<template>
  <main>
    <Form/>
  </main>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 600px;
  margin: auto;
  font-weight: normal;
}

@media (max-width: 584px) {
  #app {
    max-width: 100%;
  }
}
</style>
