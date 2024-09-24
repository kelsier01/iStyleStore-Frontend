<script setup>
<<<<<<< HEAD
import { reactive, computed, onMounted, onBeforeMount} from "vue";
=======
import { reactive, computed, onMounted, onBeforeMount } from "vue";
>>>>>>> Michael
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
<<<<<<< HEAD
import ModalMantenedorModelos from '../Modals/ModalMantenedorModelos.vue';
=======
import ModalMantenedorModelos from "../Modals/ModalMantenedorModelos.vue";
>>>>>>> Michael
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
<<<<<<< HEAD
    name:"Estado",
=======
    name: "Estado",
>>>>>>> Michael
    field: "estado",
    sort: "",
  },
  {
    name: "Acciones",
    field: "editar",
    sort: "",
  },
<<<<<<< HEAD

=======
>>>>>>> Michael
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
<<<<<<< HEAD
const estado = ref()
const modelo = ref("")
const modelos = ref()
const equipos = ref()
const modelosDispositivo = ref([])
const URL_API = import.meta.env.VITE_URL_API
=======
const estado = ref();
const modelo = ref("");
const modelos = ref();
const equipos = ref();
const modelosDispositivo = ref([]);
const URL_API = import.meta.env.VITE_URL_API;
>>>>>>> Michael
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
<<<<<<< HEAD
}

async function dataModelos(){
  await axios.get(URL_API + "modelos", token).then((response)=>{
    modelos.value = response.data.modelo
  })
  .catch(function (error) {
    Swal.fire({
=======
};

async function dataModelos() {
  await axios
    .get(URL_API + "modelos", token)
    .then((response) => {
      modelos.value = response.data.modelo;
    })
    .catch(function (error) {
      Swal.fire({
>>>>>>> Michael
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
<<<<<<< HEAD
   }); 
  await axios.get(URL_API + "equipos", token).then((response)=>{
    equipos.value = response.data.equipos
  })
  .catch(function (error) {
    Swal.fire({
=======
    });
  await axios
    .get(URL_API + "equipos", token)
    .then((response) => {
      equipos.value = response.data.equipos;
    })
    .catch(function (error) {
      Swal.fire({
>>>>>>> Michael
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
      console.log(error.response.data.msg);
<<<<<<< HEAD
   });
   const equipoDict = {};
      equipos.value.forEach(equipo => {
      equipoDict[equipo.id] = equipo.nombre;
    });

    modelosDispositivo.value = modelos.value.map(modelo => {
      return {
        ...modelo,
        nombreEquipo: equipoDict[modelo.modelo] || 'Equipo no encontrado'
      };
    });
}

onBeforeMount( () =>{
=======
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
>>>>>>> Michael
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
<<<<<<< HEAD
  console.log(modelosDispositivo)
=======
  console.log(modelosDispositivo);
>>>>>>> Michael
}
function guardarModelo() {
  dataModelos();
}

<<<<<<< HEAD

function deshabilitarModelo(id) {
  
=======
function deshabilitarModelo(id) {
>>>>>>> Michael
  Swal.fire({
    title: "¿Está seguro que desea eliminar el Dispositivo?",
    icon: "warning",
    showDenyButton: true,
    confirmButtonText: "OK",
    denyButtonText: "No",
  }).then((result) => {
    if (result.isConfirmed) {
<<<<<<< HEAD
      axios
        .delete(URL_API + "modelos/" + id, token)
        .then((response) => {
          if (response.data) {
            modelosDispositivo.value = modelosDispositivo.value.filter((modelo) => modelo.id !== id);
            Swal.fire("Cambios guardados", "", "success");
          }
        });
=======
      axios.delete(URL_API + "modelos/" + id, token).then((response) => {
        if (response.data) {
          modelosDispositivo.value = modelosDispositivo.value.filter(
            (modelo) => modelo.id !== id
          );
          Swal.fire("Cambios guardados", "", "success");
        }
      });
>>>>>>> Michael
    } else if (result.isDenied) {
      Swal.fire("Los cambios no se han guardado", "", "info");
    }
  });
}
<<<<<<< HEAD


</script>

<style lang="scss" scoped>

th{
  background-color: #45DABE;
}


=======
</script>

<style lang="scss" scoped>
th {
  background-color: #45dabe;
}

>>>>>>> Michael
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
<<<<<<< HEAD
                      <td >{{ row.nombre }}</td>
=======
                      <td>{{ row.nombre }}</td>
>>>>>>> Michael
                      <td>{{ row.nombreEquipo }}</td>
                      <td class="d-none d-xl-table-cell text-center">
                        <span
                          class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
<<<<<<< HEAD
                          :class="{'bg-success-light text-success': row.estado == 1}"
=======
                          :class="{
                            'bg-success-light text-success': row.estado == 1,
                          }"
>>>>>>> Michael
                          v-if="row.estado == 1"
                          >{{ "Habilitado" }}</span
                        >
                        <span
                          class="fs-xs fw-semibold d-inline-block py-1 px-3 rounded-pill"
<<<<<<< HEAD
                          :class="{'bg-success-light text-warning': row.estado == 0}"
=======
                          :class="{
                            'bg-success-light text-warning': row.estado == 0,
                          }"
>>>>>>> Michael
                          v-else-if="row.estado == 0"
                          >{{ "Deshabilitado" }}</span
                        >
                      </td>
<<<<<<< HEAD
                      <td >
=======
                      <td>
>>>>>>> Michael
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
<<<<<<< HEAD
                            v-if="row.estado == null || row.nombre == '' || row.modelo == null"
=======
                            v-if="
                              row.estado == null ||
                              row.nombre == '' ||
                              row.modelo == null
                            "
>>>>>>> Michael
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
