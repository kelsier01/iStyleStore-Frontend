<script setup>
import { computed, onMounted, ref } from "vue";
import axios from "axios";
import moment from "moment";
import { useRouter } from "vue-router";

// Helper variables
const rutaAPI = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
const orderSearch = ref(false);
const ordenes = ref("");
const selectEstado = ref(null);
const selectFecha = ref(null);
const router = useRouter();
const onlyOrdenes = ref(null);

onMounted(() => {
  axios
    .get(rutaAPI + "ordenes", token)
    .then((response) => {
      console.log(response.data);
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

function filtrarOrdenes(estado) {
  selectEstado.value = estado;
}

function SelectDFilter(dias) {
  selectFecha.value = dias;
}

function verOrden(value) {
  router.push({
    name: "revision",
    query: { idOrden: value },
  });
}

function abrirPDF(value) {
  router.push({
    name: "ordenpdf",
    query: { idOrden: value },
  });
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
        <!-- END Conversion Rate-->
      </div>
    </div>
    <!-- END Overview -->

    <!-- Statistics -->

    <!-- END Statistics -->

    <!-- Recent Orders -->
    <BaseBlock title="Recent Orders">
      <template #options>
        <div class="space-x-1">
          <button
            type="button"
            class="btn btn-sm btn-alt-secondary"
            @click="
              () => {
                orderSearch = !orderSearch;
              }
            "
          >
            <i class="fa fa-search"></i>
          </button>
          <div class="dropdown d-inline-block">
            <button
              type="button"
              class="btn btn-sm btn-alt-secondary"
              id="dropdown-recent-orders-filters"
              data-bs-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
              :class="{ 'bg-primary': selectFecha }"
            >
              <i class="fa fa-fw fa-flask"></i>
              Filters
              <i class="fa fa-angle-down ms-1"></i>
            </button>
            <div
              class="dropdown-menu dropdown-menu-md dropdown-menu-end fs-sm"
              aria-labelledby="dropdown-recent-orders-filters"
            >
              <a
                class="dropdown-item fw-medium d-flex align-items-center justify-content-between"
                @click="SelectDFilter(1)"
              >
                Día
                <!-- <span class="badge bg-primary rounded-pill">{{
                  ordenes.totalIniciadas
                }}</span> -->
                <span
                  class="badge bg-primary rounded-pill"
                  v-show="selectFecha == 1"
                >
                  <i class="far fa-circle-check"></i>
                </span>
              </a>
              <a
                class="dropdown-item fw-medium d-flex align-items-center justify-content-between"
                @click="SelectDFilter(7)"
              >
                Semana
                <span
                  class="badge bg-primary rounded-pill"
                  v-show="selectFecha == 7"
                >
                  <i class="far fa-circle-check"></i>
                </span>
              </a>
              <a
                class="dropdown-item fw-medium d-flex align-items-center justify-content-between"
                @click="SelectDFilter(30)"
              >
                Mes
                <span
                  class="badge bg-primary rounded-pill"
                  v-show="selectFecha == 30"
                >
                  <i class="far fa-circle-check"></i>
                </span>
              </a>
              <a
                class="dropdown-item fw-medium d-flex align-items-center justify-content-between"
                @click="SelectDFilter(null)"
              >
                Todas
                <span
                  class="badge bg-primary rounded-pill"
                  v-show="!selectFecha"
                >
                  <i class="far fa-circle-check"></i>
                </span>
              </a>
            </div>
          </div>
        </div>
      </template>

      <template #content>
        <div
          v-if="orderSearch"
          id="one-dashboard-search-orders"
          class="block-content border-bottom"
        >
          <!-- Search Form -->
          <form @submit.prevent>
            <div class="push">
              <div class="input-group">
                <input
                  type="text"
                  class="form-control form-control-alt"
                  id="one-ecom-orders-search"
                  name="one-ecom-orders-search"
                  placeholder="Search all orders.."
                />
                <span class="input-group-text bg-body border-0">
                  <i class="fa fa-search"></i>
                </span>
              </div>
            </div>
          </form>
          <!-- END Search Form -->
        </div>
        <div class="block-content block-content-full">
          <!-- Recent Orders Table -->
          <div class="table-responsive">
            <table class="table table-hover table-vcenter">
              <thead>
                <tr>
                  <th>Orden Nº</th>
                  <th class="d-none d-xl-table-cell">Cliente</th>
                  <th class="d-none d-sm-table-cell">Dispositivo</th>
                  <th class="d-none d-sm-table-cell text-center">
                    Estado Orden
                  </th>
                  <th class="d-none d-sm-table-cell text-center">Ingreso</th>
                  <th class="d-none d-sm-table-cell text-center">Entrega</th>
                  <th class="d-none d-sm-table-cell text-center">Valor</th>
                  <th class="d-none d-sm-table-cell text-center"></th>
                </tr>
              </thead>
              <tbody class="fs-sm">
                <tr v-for="orden in getOrdenes" :key="orden.id">
                  <td>
                    <a class="fw-semibold" href="javascript:void(0)"> ORDEN </a>
                    <p class="fs-sm fw-medium text-muted mb-0">
                      {{ orden.id }}
                    </p>
                  </td>
                  <td class="d-none d-xl-table-cell">
                    <a class="fw-semibold" href="javascript:void(0)"></a>
                    <p class="fs-sm fw-medium text-muted mb-0">
                      {{ orden.Cliente.nombre }}
                    </p>
                  </td>
                  <td class="d-none d-xl-table-cell">
                    <a class="fw-semibold" href="javascript:void(0)">{{
                      orden.Equipo.nombre
                    }}</a>
                    <p class="fs-sm fw-medium text-muted mb-0">
                      {{ orden.Dispositivo.nombre }}
                    </p>
                  </td>
                  <td class="d-none d-xl-table-cell text-center">
                    <span
                      class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
                      :class="{
                        'bg-success-light text-success': orden.estado == 3,
                        'bg-info-light text-info': orden.estado == 2,
                        'bg-warning-light text-warning': orden.estado == 1,
                      }"
                      >{{ orden.estados_ordene.nombre_estado }}</span
                    >
                  </td>
                  <td
                    class="d-none d-sm-table-cell fw-semibold text-muted text-center"
                  >
                    {{ moment(orden.created_at).format("DD/MM/YYYY LT") }}
                  </td>
                  <td
                    class="d-none d-sm-table-cell fw-semibold text-muted text-center"
                  >
                    {{ orden.fecha_entrega || "Sin fecha." }}
                  </td>
                  <td class="d-none d-sm-table-cell text-center">
                    <strong>
                      $
                      {{
                        orden.total
                          .toString()
                          .replace(/\B(?=(\d{3})+(?!\d))/g, ".")
                      }}</strong
                    >
                  </td>
                  <td>
                    <span class="ms-5 pointer" @click="verOrden(orden.id)">
                      <i class="far fa-2x fa-eye"></i>
                    </span>
                  </td>
                  <td>
                    <span class="ms-5 pointer" @click="abrirPDF(orden.id)">
                      <i class="fa fa-2x fa-file-pdf"></i>
                    </span>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
          <!-- END Recent Orders Table -->
        </div>
        <div class="block-content block-content-full bg-body-light">
          <!-- Pagination -->
          <nav aria-label="Photos Search Navigation">
            <ul class="pagination pagination-sm justify-content-end mb-0">
              <li class="page-item">
                <a
                  class="page-link"
                  href="javascript:void(0)"
                  tabindex="-1"
                  aria-label="Previous"
                >
                  Prev
                </a>
              </li>
              <li class="page-item active">
                <a class="page-link" href="javascript:void(0)">1</a>
              </li>
              <li class="page-item">
                <a class="page-link" href="javascript:void(0)">2</a>
              </li>
              <li class="page-item">
                <a class="page-link" href="javascript:void(0)">3</a>
              </li>
              <li class="page-item">
                <a class="page-link" href="javascript:void(0)">4</a>
              </li>
              <li class="page-item">
                <a
                  class="page-link"
                  href="javascript:void(0)"
                  aria-label="Next"
                >
                  Next
                </a>
              </li>
            </ul>
          </nav>
          <!-- END Pagination -->
        </div>
      </template>
    </BaseBlock>
    <!-- END Recent Orders -->
  </div>
  <!-- END Page Content -->
</template>

<style scoped>
.pointer {
  cursor: pointer;
}
</style>
