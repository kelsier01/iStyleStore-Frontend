<script setup>
import ListarOrdenesTable from "./Components/Tables/ListarOrdenesTable.vue";
</script>

<template>
  <!-- Page Content -->
  <div class="content">
    <ListarOrdenesTable />
  </div>
</template>

<style>
@media (min-width: 1200px) {
  #page-container.main-content-narrow > #main-container .content {
    width: 100%;
  }
}
</style>
