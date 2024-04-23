<script setup>
import FormRevision from "./Components/Forms/FormRevision.vue";
import RevisionHistorialTable from "./Components/Tables/RevisionHistorialTable.vue";
import FormRevisionDiagnostico from "./Components/Forms/FormRevisionDiagnostico.vue";
import FormRevisionProducto from "./Components/Forms/FormRevisionProducto.vue";
</script>

<template>


  <!-- Page Content -->
  <div class="content">
    <BaseBlock title="Revision">
      <FormRevision />
    </BaseBlock>
    <BaseBlock>
      <RevisionHistorialTable />
    </BaseBlock>
    <BaseBlock >
      <FormRevisionDiagnostico />
    </BaseBlock>
    <BaseBlock>
      <FormRevisionProducto /> 
    </BaseBlock>
  </div>
  <!-- END Page Content -->
</template>
