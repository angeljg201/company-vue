<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import Nav from './components/Nav.vue';
</script>

<template>
  <Nav />
  <div class="container-fluid mt-3">
  </div>
  <RouterView />
</template>