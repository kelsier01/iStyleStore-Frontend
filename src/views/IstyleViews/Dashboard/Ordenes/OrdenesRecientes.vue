<script setup>
import { reactive, computed, onMounted, ref, onBeforeMount, defineProps, watch } from "vue";
import axios from "axios";
import moment from "moment";
import { useRouter } from "vue-router";
// Vue Dataset, for more info and examples you can check out https://github.com/kouts/vue-dataset/tree/next
import {
  Dataset,
  DatasetItem,
  DatasetInfo,
  DatasetPager,
  DatasetSearch,
  DatasetShow,
} from "vue-dataset";

//Instancia una variable dinamica y la ruta de la API
const router = useRouter();
const ordenes = ref([]);
const rutaAPI = import.meta.env.VITE_URL_API;
const filtroSeleccionado = ref(3);

// const router = useRouter();
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
// Variables tabla
const getDatosFiltrados = ref();
const estado_tabla_id = ref();

//Props
const props = defineProps(['estado_orden']);
watch(() => props.estado_orden, (nuevoValor) => {
  estado_tabla_id.value = nuevoValor;
  console.log("Cambio en estado_orden:", estado_tabla_id.value);
  filtrarOrdenes();
});



const cargarDataTable = () => {
  axios
    .get(rutaAPI + "ordenes/pendientes", token)
    .then((response) => {
      console.log(response.data.ordenes);
      ordenes.value = response.data.ordenes.reverse().map((orden) => {
        return {
          id: orden.id,
          cliente: orden.Cliente.nombre,
          equipo: orden.Equipo.nombre,
          dispositivo: orden.Dispositivo.nombre,
          estado_orden_id: orden.estados_ordene.id,
          estado_orden_nombre: orden.estados_ordene.nombre_estado,
          fecha_ingreso: moment(orden.created_at).format("DD/MM/YYYY"),
          fecha_entrega: moment(orden.fecha_entrega).format("DD/MM/YYYY"),
          valor: orden.total.toString().replace(/\B(?=(\d{3})+(?!\d))/g, "."),
          valor_recepcion: orden.total_recepcion.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
        };
      });
      getDatosFiltrados.value = ordenes.value;
    })
    .catch((e) => {
      console.error("Error al cargar las órdenes:", e);
    });
};

const verOrden = (value) => {
  router.push({
    name: "revision",
    query: { idOrden: value },
  });
};

// Helper variables
const cols = reactive([
  {
    name: "Cliente",
    field: "cliente",
    sort: "",
  },
  {
    name: "Dispositivo",
    field: "dispositivo",
    sort: "",
  },
  {
    name: "Estado orden",
    field: "estado_orden",
    sort: "",
  },
  {
    name: "Ingreso",
    field: "ingreso",
    sort: "",
  },
  {
    name: "Entrega",
    field: "entrega",
    sort: "",
  },
  {
    name: "Valor",
    field: "valor",
    sort: "",
  },
]);

// Sort by functionality
const sortBy = computed(() => {
  return cols.reduce((acc, o) => {
    if (o.sort) {
      o.sort === "asc" ? acc.push(o.field) : acc.push("-" + o.field);
    }
    return acc;
  }, []);
});

// On sort th click
function onSort(event, i) {
  let toset;
  const sortEl = cols[i];

  if (!event.shiftKey) {
    cols.forEach((o) => {
      if (o.field !== sortEl.field) {
        o.sort = "";
      }
    });
  }

  if (!sortEl.sort) {
    toset = "asc";
  }

  if (sortEl.sort === "desc") {
    toset = event.shiftKey ? "" : "asc";
  }

  if (sortEl.sort === "asc") {
    toset = "desc";
  }

  sortEl.sort = toset;
}

// Traer lista de clientes

onBeforeMount(() => {
  cargarDataTable();
});

onMounted(() => {
  // Remove labels from
  document.querySelectorAll("#datasetLength label").forEach((el) => {
    el.remove();
  });

  // Replace select classes
  let selectLength = document.querySelector("#datasetLength select");
  selectLength.classList = "";
  selectLength.classList.add("form-select");
  selectLength.style.width = "80px";
});

const filtrarOrdenes = () => {
  const getHoy = moment().format("DD/MM/YYYY");
  const semanaPasada = moment().subtract(7, "days").format("DD/MM/YYYY");
  const ultimoMes = moment().subtract(1, "months").format("DD/MM/YYYY");

  console.log("Hoy es: ", getHoy);
  console.log("Semana pasada: ", semanaPasada);
  console.log("Hace un mes: ", ultimoMes);
  console.log("Opcion seleccionada: ", filtroSeleccionado.value);

  if (getDatosFiltrados.value) {
    const filtrarPorEstado = (orden) => {
      return estado_tabla_id.value == null || orden.estado_orden_id == estado_tabla_id.value;
    }

    if (filtroSeleccionado.value == 0) {
      console.log("Dentro de DIA");
      getDatosFiltrados.value = ordenes.value.filter((orden) => {
        return orden.fecha_ingreso == getHoy && filtrarPorEstado(orden);
      });
    } else if (filtroSeleccionado.value == 1) {
      const convertirFecha = (fecha) => {
        const [dia, mes, año] = fecha.split("/");
        return new Date(`${año}-${mes}-${dia}`);
      };

      const semanaPasadaDate = new Date();
      semanaPasadaDate.setDate(semanaPasadaDate.getDate() - 7); // Ajustar según la semana anterior
      const hoy = convertirFecha(getHoy);

      getDatosFiltrados.value = ordenes.value.filter((orden) => {
        const fechaOrden = convertirFecha(orden.fecha_ingreso);
        return fechaOrden >= semanaPasadaDate && fechaOrden <= hoy && filtrarPorEstado(orden);
      });
    } else if (filtroSeleccionado.value == 2) {
      // Filtro para el último mes
      const convertirFecha = (fecha) => {
        const [dia, mes, año] = fecha.split("/");
        return new Date(`${año}-${mes}-${dia}`);
      };

      const ultimoMesDate = new Date();
      ultimoMesDate.setMonth(ultimoMesDate.getMonth() - 1); // Restar 1 mes
      const hoy = convertirFecha(getHoy);

      getDatosFiltrados.value = ordenes.value.filter((orden) => {
        const fechaOrden = convertirFecha(orden.fecha_ingreso);
        return fechaOrden >= ultimoMesDate && fechaOrden <= hoy && filtrarPorEstado(orden);
      });
    } else if (filtroSeleccionado.value == 3) {
      // Si no hay filtro de tiempo, solo filtra por estado
      getDatosFiltrados.value = ordenes.value.filter(filtrarPorEstado);
    }
  }
  console.log(getDatosFiltrados);
};


</script>

<template>
  <Dataset
    v-slot="{ ds }"
    :ds-data="getDatosFiltrados"
    :ds-sortby="sortBy"
    :ds-search-in="[
      'cliente',
      'dispositivo',
      'estado_orden_nombre',
      'fecha_ingreso',
      'fecha_entrega',
      'valor',
    ]"
  >
    <div class="row" :data-page-count="ds.dsPagecount">
      <div id="datasetLength" class="col-md-8 py-2">
        <DatasetShow />
      </div>
      <div class="row">
        <div class="col-md-2">
          <select
            @change="filtrarOrdenes"
            v-model="filtroSeleccionado"
            class="form-select"
          >
            <option value="0" selected>Día</option>
            <option value="1">Semana</option>
            <option value="2">Mes</option>
            <option value="3">Todos</option>
          </select>
        </div>
        <div class="col-md-7"></div>
        <div class="col-md-3">
          <DatasetSearch ds-search-placeholder="Buscar..." />
        </div>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col-md-12">
        <div class="table-responsive">
          <table class="table table-hover table-vcenter">
            <thead>
              <tr>
                <th scope="col">N° DE ORDEN</th>
                <th
                  v-for="(th, index) in cols"
                  :key="th.field"
                  :class="['sort', th.sort]"
                  @click="onSort($event, index)"
                >
                  {{ th.name }}
                </th>
              </tr>
            </thead>
            <DatasetItem tag="tbody" class="fs-sm">
              <template #default="{ row }">
                <tr @click="verOrden(row.id)" class="pointer">
                  <td scope="row">{{ row.id }}</td>
                  <td class="d-none d-xl-table-cell">
                    {{ row.cliente }}
                  </td>
                  <td class="d-none d-xl-table-cell">
                    <a class="fw-semibold" href="javascript:void(0)">{{
                      row.equipo
                    }}</a>
                    <p class="fs-sm fw-medium text-muted mb-0">
                      {{ row.dispositivo }}
                    </p>
                  </td>
                  <td class="d-none d-xl-table-cell text-center">
                    <span
                      class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
                      :class="{
                        'bg-primary-light text-info': row.estado_orden_id === 4,
                        'bg-success-light text-success':
                          row.estado_orden_id === 3,
                        'bg-info-light text-info': row.estado_orden_id === 2,
                        'bg-warning-light text-warning':
                          row.estado_orden_id === 1,
                      }"
                      >{{ row.estado_orden_nombre }}</span
                    >
                  </td>
                  <td
                    class="d-none d-sm-table-cell fw-semibold text-muted text-center"
                  >
                    {{ row.fecha_ingreso }}
                  </td>
                  <td
                    class="d-none d-sm-table-cell fw-semibold text-muted text-center"
                  >
                    {{ row.fecha_entrega || "Sin fecha." }}
                  </td>
                  <td class="d-none d-sm-table-cell text-center">
                    <strong> {{ row.valor == 0 ? row.valor_recepcion : row.valor }}</strong>
                  </td>
                </tr>
              </template>
            </DatasetItem>
          </table>
        </div>
      </div>
    </div>
    <div
      class="d-flex flex-md-row flex-column justify-content-between align-items-center"
    >
      <DatasetInfo class="py-3 fs-sm" />
      <DatasetPager class="flex-wrap py-3 fs-sm" />
    </div>
  </Dataset>
</template>
<style lang="scss" scoped>
.gg-select {
  box-sizing: border-box;
  position: relative;
  display: block;
  transform: scale(1);
  width: 22px;
  height: 22px;
}
.gg-select::after,
.gg-select::before {
  content: "";
  display: block;
  box-sizing: border-box;
  position: absolute;
  width: 8px;
  height: 8px;
  left: 7px;
  transform: rotate(-45deg);
}
.gg-select::before {
  border-left: 2px solid;
  border-bottom: 2px solid;
  bottom: 4px;
  opacity: 0.3;
}
.gg-select::after {
  border-right: 2px solid;
  border-top: 2px solid;
  top: 4px;
  opacity: 0.3;
}
th.sort {
  cursor: pointer;
  user-select: none;
  &.asc {
    .gg-select::after {
      opacity: 1;
    }
  }
  &.desc {
    .gg-select::before {
      opacity: 1;
    }
  }
}
#page-container.main-content-narrow > #main-container .content {
  width: 100%;
}
.pointer {
  cursor: pointer;
}
</style>
