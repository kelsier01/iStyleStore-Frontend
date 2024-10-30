<script setup>
import { computed, onBeforeMount, ref } from "vue";
import axios from "axios";
import moment from "moment";
import { useRouter } from "vue-router";
import OrdenesTable from "./OrdenesTable.vue";

// Helper variables
const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const orderSearch = ref(false);
const ordenes = ref({});
const selectEstado = ref(null);
const selectFecha = ref(null);
const router = useRouter();
const onlyOrdenes = ref([]);

onBeforeMount(() => {
  axios
    .get(rutaAPI + "ordenes", token)
    .then((response) => {
      ordenes.value = response.data;
      console.log("Ordenes: ",response.data);
      onlyOrdenes.value = response.data.ordenes;
    })
    .catch((error) => {
      console.log(error);
    });
});

const getOrdenes = computed(() => {
  let hoy = moment();
  let fecha_anterior = moment().add(-selectFecha.value, "days");

  if (!selectEstado.value && !selectFecha.value) {
    return onlyOrdenes.value;
  } else if (selectEstado.value && !selectFecha.value) {
    return onlyOrdenes.value.filter(
      (item) => item.estado == selectEstado.value
    );
  } else if (!selectEstado.value && selectFecha.value) {
    return onlyOrdenes.value.filter((item) =>
      moment(item.created_at).isBetween(fecha_anterior, hoy)
    );
  }

  return onlyOrdenes.value.filter(
    (item) =>
      item.estado == selectEstado.value &&
      moment(item.created_at).isBetween(fecha_anterior, hoy)
  );
});

function filtrarOrdenes(estado) {
  selectEstado.value = estado;
}

</script>

<template>
  <!-- Hero -->
  <div class="content">
    <div
      class="d-flex flex-column flex-md-row justify-content-md-between align-items-md-center py-2 text-center text-md-start"
    >
      <div class="flex-grow-1 mb-1 mb-md-0">
        <h1 class="h3 fw-bold mb-2">Ordenes Pendientes</h1>
      </div>
    </div>
  </div>
  <!-- END Hero -->

  <!-- Page Content -->
  <div class="content">
    <!-- Overview -->
    <div class="row items-push">
      <div class="col-12">
        <!-- Conversion Rate -->
        <BaseBlock class="d-flex flex-column h-100 mb-0">
          <template #content>
            <div
              class="block-content block-content-full flex-grow-1 d-flex justify-content-between align-items-center"
            >
              <dl class="mb-0">
                <dt class="fs-3 fw-bold">{{ ordenes.total }}</dt>
                <dd class="fs-sm fw-medium fs-sm fw-medium text-muted mb-0">
                  Total de Ordenes
                </dd>
              </dl>
              <div class="item item-rounded-lg bg-body-light">
                <i class="fa fa-chart-bar fs-3 text-primary"></i>
              </div>
            </div>
            <div class="bg-body-light rounded-bottom">
              <a
                class="block-content block-content-full block-content-sm fs-sm fw-medium d-flex align-items-center justify-content-between pointer"
                @click="filtrarOrdenes(null)"
              >
                <span>Ver Todas las ordenes</span>
                <i
                  class="fa fa-arrow-alt-circle-right ms-1 opacity-25 fs-base"
                ></i>
              </a>
            </div>
          </template>
        </BaseBlock>
      </div>
    </div>
    <BaseBlock>
      <OrdenesTable />
    </BaseBlock>
  </div>
  </template>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>
