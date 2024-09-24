<script setup>
import { useRoute } from "vue-router";
import FormRevision from "./Components/Forms/FormRevision.vue";
import { onMounted, ref } from "vue";
const route = useRoute();
const id = ref(null);
if (route.query.idOrden) {
  id.value = route.query.idOrden;
}
onMounted(() => {});
</script>

<template>
  <!-- Page Content -->
  <div class="content">
    <FormRevision :idOrden="id" />
  </div>
  <!-- END Page Content -->
</template>
<style>
@media (min-width: 1200px) {
  #page-container.main-content-narrow > #main-container .content {
    width: 100%;
  }
}
.form-control {
  height: auto;
}
.large-textarea {
  border: 1px solid #63c9ad !important;
  border-radius: 20px !important;
}
</style>
