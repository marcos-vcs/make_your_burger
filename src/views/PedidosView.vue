<template>
  <div class="main-container">
    <h1>Gerenciar pedidos:</h1>
    <dashboard></dashboard>
  </div>
</template>

<script>
import Dashboard from '@/components/Dashboard.vue';

export default {
  name: 'PedidosView',
  components: {
    Dashboard,
  }
}
</script>

<style scoped>

</style>
