<script setup>
import { reactive, computed, onMounted, onBeforeMount } from "vue";
import axios from "axios";
import Swal from "sweetalert2";
// Vue Dataset, for more info and examples you can check out https://github.com/kouts/vue-dataset/tree/next
import {
  Dataset,
  DatasetItem,
  DatasetInfo,
  DatasetPager,
  DatasetSearch,
  DatasetShow,
} from "vue-dataset";
import ModalMantenedorModelos from "../Modals/ModalMantenedorModelos.vue";
import { ref } from "vue";
// Helper variables
const cols = reactive([
  {
    name: "Nombre",
    field: "nombre",
    sort: "",
  },
  {
    name: "Modelo",
    field: "modelo",
    sort: "",
  },
  {
    name: "Estado",
    field: "estado",
    sort: "",
  },
  {
    name: "Acciones",
    field: "editar",
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
const estado = ref();
const modelo = ref("");
const modelos = ref();
const equipos = ref();
const modelosDispositivo = ref([]);
const URL_API = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};

async function dataModelos() {
  await axios
    .get(URL_API + "modelos", token)
    .then((response) => {
      modelos.value = response.data.modelo;
    })
    .catch(function (error) {
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
    });
  await axios
    .get(URL_API + "equipos", token)
    .then((response) => {
      equipos.value = response.data.equipos;
    })
    .catch(function (error) {
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
    });
  const equipoDict = {};
  equipos.value.forEach((equipo) => {
    equipoDict[equipo.id] = equipo.nombre;
  });

  modelosDispositivo.value = modelos.value.map((modelo) => {
    return {
      ...modelo,
      nombreEquipo: equipoDict[modelo.modelo] || "Equipo no encontrado",
    };
  });
}

onBeforeMount(() => {
  dataModelos();
});
// Apply a few Bootstrap 5 optimizations
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

function abrirModal(data) {
  estado.value = 0;
  modelo.value = data;
}
function abrirModalGuardar() {
  estado.value = 1;
}
function updateModelo(data) {
  const idx = modelosDispositivo.value.findIndex((val) => val.id === data.id);
  // update it using the index
  modelosDispositivo.value[idx] = data;
  console.log(modelosDispositivo);
}
function guardarModelo() {
  dataModelos();
}

function deshabilitarModelo(id) {
  Swal.fire({
    title: "¿Está seguro que desea eliminar el Dispositivo?",
    icon: "warning",
    showDenyButton: true,
    confirmButtonText: "OK",
    denyButtonText: "No",
  }).then((result) => {
    if (result.isConfirmed) {
      axios.delete(URL_API + "modelos/" + id, token).then((response) => {
        if (response.data) {
          modelosDispositivo.value = modelosDispositivo.value.filter(
            (modelo) => modelo.id !== id
          );
          Swal.fire("Cambios guardados", "", "success");
        }
      });
    } else if (result.isDenied) {
      Swal.fire("Los cambios no se han guardado", "", "info");
    }
  });
}
</script>

<style lang="scss" scoped>
th {
  background-color: #45dabe;
}

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
</style>

<template>
  <button
    type="button"
    class="btn btn-dark col-1 offset-11 waves-effect waves-light"
    data-bs-toggle="modal"
    data-bs-target="#modal-block-small"
    @click="abrirModalGuardar()"
  >
    Agregar
  </button>
  <!-- Page Content -->
  <div class="content">
    <ModalMantenedorModelos
      :estado="estado"
      :dataModelo="modelo"
      :dataEquipo="equipos"
      @updateModelo="updateModelo"
      @guardarModelo="guardarModelo"
    />
    <BaseBlock content-full>
      <Dataset
        v-slot="{ ds }"
        :ds-data="modelosDispositivo"
        :ds-sortby="sortBy"
        :ds-search-in="['nombre', 'modelo']"
      >
        <div class="row" :data-page-count="ds.dsPagecount">
          <div id="datasetLength" class="col-md-8 py-2">
            <DatasetShow />
          </div>
          <div class="col-md-4 py-2">
            <DatasetSearch ds-search-placeholder="Search..." />
          </div>
        </div>
        <hr />
        <div class="row">
          <div class="col-md-12">
            <div class="table-responsive">
              <table class="table table-striped mb-0">
                <thead>
                  <tr>
                    <th scope="col">N°</th>
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
                  <template #default="{ row, rowIndex }">
                    <tr>
                      <td scope="row">{{ rowIndex + 1 }}</td>
                      <td>{{ row.nombre }}</td>
                      <td>{{ row.nombreEquipo }}</td>
                      <td class="d-none d-xl-table-cell text-center">
                        <span
                          class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
                          :class="{
                            'bg-success-light text-success': row.estado == 1,
                          }"
                          v-if="row.estado == 1"
                          >{{ "Habilitado" }}</span
                        >
                        <span
                          class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
                          :class="{
                            'bg-success-light text-warning': row.estado == 0,
                          }"
                          v-else-if="row.estado == 0"
                          >{{ "Deshabilitado" }}</span
                        >
                      </td>
                      <td>
                        <div class="btn-group">
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            data-bs-toggle="modal"
                            data-bs-target="#modal-block-small"
                            @click="abrirModal(row)"
                          >
                            <i class="fa fa-fw fa-pencil-alt"></i>
                          </button>
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            @click="deshabilitarModelo(row.id)"
                            v-if="
                              row.estado == null ||
                              row.nombre == '' ||
                              row.modelo == null
                            "
                          >
                            <i class="fa fa-fw fa-times"></i>
                          </button>
                        </div>
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
    </BaseBlock>
  </div>
  <!-- END Page Content -->
</template>
