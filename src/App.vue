<script setup>
import MenuComponente from './components/MenuComponente.vue';
</script>

<template>
  <main class="principal">
    <MenuComponente/>  

    <RouterView />
  </main>

</template>

<style scoped>
.principal{
  display: flex;
  height: 100vh;
gap:20px;
  
}
</style>
