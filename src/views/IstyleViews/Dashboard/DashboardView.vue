<script setup>
import { computed, onMounted, ref } from "vue";
import axios from "axios";
import moment from "moment";
import { useRouter } from "vue-router";
import OrdenesRecientes from "./Ordenes/OrdenesRecientes.vue"

// Helper variables
const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};

const ordenes = ref("");
const selectEstado = ref(null);
const selectFecha = ref(null);
const router = useRouter();
const onlyOrdenes = ref(null);

onMounted(() => {
  axios
    .get(rutaAPI + "ordenes/pendientes", token)
    .then((response) => {
      response.data.suma =
        response.data.totalIniciadas +
        response.data.totalRevision +
        response.data.totalRetiro;
      ordenes.value = response.data;
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

const estado_orden_id = ref();

const estado_orden = (id) =>{
  estado_orden_id.value = id; 
  console.log(estado_orden_id.value)
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
      <div class="col-sm-6 col-xxl-3">
        <!-- Pending Orders -->
        <BaseBlock class="d-flex flex-column h-100 mb-0">
          <template #content>
            <div
              class="block-content block-content-full flex-grow-1 d-flex justify-content-between align-items-center"
            >
              <dl class="mb-0">
                <dt class="fs-3 fw-bold">{{ ordenes.totalIniciadas }}</dt>
                <dd class="fs-sm fw-medium fs-sm fw-medium text-muted mb-0">
                  Ordenes Sin Revisar
                </dd>
              </dl>
              <div class="item item-rounded-lg bg-body-light">
                <i class="far fa-gem fs-3 text-primary"></i>
              </div>
            </div>
            <div
              class="rounded-bottom"
              :class="selectEstado == 1 ? 'bg-dark' : 'bg-body-light'"
            >
              <a
                class="block-content block-content-full block-content-sm fs-sm fw-medium d-flex align-items-center justify-content-between pointer"
                @click="estado_orden(1)"
              >
                <span>Ver Ordenes sin revisión</span>
                <i
                  class="fa fa-arrow-alt-circle-right ms-1 opacity-25 fs-base"
                ></i>
              </a>
            </div>
          </template>
        </BaseBlock>
        <!-- END Pending Orders -->
      </div>
      <div class="col-sm-6 col-xxl-3">
        <!-- New Customers -->
        <BaseBlock class="d-flex flex-column h-100 mb-0">
          <template #content>
            <div
              class="block-content block-content-full flex-grow-1 d-flex justify-content-between align-items-center"
            >
              <dl class="mb-0">
                <dt class="fs-3 fw-bold">{{ ordenes.totalRevision }}</dt>
                <dd class="fs-sm fw-medium fs-sm fw-medium text-muted mb-0">
                  Ordenes en Revisión
                </dd>
              </dl>
              <div class="item item-rounded-lg bg-body-light">
                <i class="far fa-user-circle fs-3 text-primary"></i>
              </div>
            </div>
            <div
              class="rounded-bottom"
              :class="selectEstado == 2 ? 'bg-dark' : 'bg-body-light'"
            >
              <a
                class="block-content block-content-full block-content-sm fs-sm fw-medium d-flex align-items-center justify-content-between pointer"
                @click="estado_orden(2)"
              >
                <span>Ver Ordenes en revisión</span>
                <i
                  class="fa fa-arrow-alt-circle-right ms-1 opacity-25 fs-base"
                ></i>
              </a>
            </div>
          </template>
        </BaseBlock>
        <!-- END New Customers -->
      </div>
      <div class="col-sm-6 col-xxl-3">
        <!-- Messages -->
        <BaseBlock class="d-flex flex-column h-100 mb-0">
          <template #content>
            <div
              class="block-content block-content-full flex-grow-1 d-flex justify-content-between align-items-center"
            >
              <dl class="mb-0">
                <dt class="fs-3 fw-bold">{{ ordenes.totalRetiro }}</dt>
                <dd class="fs-sm fw-medium fs-sm fw-medium text-muted mb-0">
                  Ordenes para Retiro
                </dd>
              </dl>
              <div class="item item-rounded-lg bg-body-light">
                <i class="far fa-paper-plane fs-3 text-primary"></i>
              </div>
            </div>
            <div
              class="rounded-bottom"
              :class="selectEstado == 3 ? 'bg-dark' : 'bg-body-light'"
            >
              <a
                class="block-content block-content-full block-content-sm fs-sm fw-medium d-flex align-items-center justify-content-between pointer"
                @click="estado_orden(3)"
              >
                <span>Ver Ordenes para retiro</span>
                <i
                  class="fa fa-arrow-alt-circle-right ms-1 opacity-25 fs-base"
                ></i>
              </a>
            </div>
          </template>
        </BaseBlock>
        <!-- END Messages -->
      </div>
      <div class="col-sm-6 col-xxl-3">
        <!-- Conversion Rate -->
        <BaseBlock class="d-flex flex-column h-100 mb-0">
          <template #content>
            <div
              class="block-content block-content-full flex-grow-1 d-flex justify-content-between align-items-center"
            >
              <dl class="mb-0">
                <dt class="fs-3 fw-bold">{{ ordenes.suma }}</dt>
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
                @click="estado_orden(null)"
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

    <!-- Ordenes Recientes -->
    <BaseBlock title="Ordenes Recientes" content-full>
      <OrdenesRecientes :estado_orden="estado_orden_id"/>
    </BaseBlock>
  </div>
</template>

<style scoped>

</style>
