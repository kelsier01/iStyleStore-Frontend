<script setup>
import FormRecepcionEquipos from "./Components/Forms/FormRecepcionEquipos.vue";
import FormEstadoDelEquipo from "./Components/Forms/FormEstadoDelEquipo.vue";

</script>

<template>

  <!-- Page Content -->
  <div class="content">
    <BaseBlock title="Protocolo de recepción de equipos">
      <FormRecepcionEquipos />
    </BaseBlock>
    <BaseBlock title="Estado del equipo">
      <FormEstadoDelEquipo />
    </BaseBlock>
  </div>
  <!-- END Page Content -->
</template>
