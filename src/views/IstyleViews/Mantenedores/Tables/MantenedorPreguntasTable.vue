<script setup>
import { reactive, computed, onMounted, onBeforeMount, onUpdated } from "vue";

// Vue Dataset, for more info and examples you can check out https://github.com/kouts/vue-dataset/tree/next
import {
  Dataset,
  DatasetItem,
  DatasetInfo,
  DatasetPager,
  DatasetSearch,
  DatasetShow,
} from "vue-dataset";

import ModalMantenedorPreguntas from "../Modals/ModalMantenedorPreguntas.vue";
import axios from "axios";
import { ref } from "vue";
import Swal from "sweetalert2";
// Helper variables
const cols = reactive([
  {
    name: "Acciones",
    field: "acciones",
    sort: "",
  },
  {
    name: "Preguntas",
    field: "pregunta",
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


const estado_modal = ref(0);
const pregunta_modal = ref('');
const equipo_estado = ref(1);
const equipo_has_preguntas = ref();
const equipos = ref();
const preguntas = ref();
const URL_API = import.meta.env.VITE_URL_API;
const token = {
  headers: {
    "x-token": localStorage.getItem("Token"),
  },
};
//Traer Equipo_Has_Preguntas
const getDataEquipo_Has_Pregunta = async () => {
  await axios
    .get(URL_API + "equipo_preguntas/", token)
    .then((response) => {
      if (response) {
        equipo_has_preguntas.value = response.data.preguntas;
        console.log(equipo_has_preguntas.value);
      }
    })
    .catch((error) => {
      console.log(error);
    });
};
// Traer equipos
const getEquipos = async () => {
  await axios
    .get(URL_API + "equipos/", token)
    .then((response) => {
      if (response) {
        equipos.value = response.data.equipos;
        theaders();
      }
    })
    .catch((error) => {
      console.log(error);
    });
};

//Traer preguntas
const getPreguntas = async () => {
  await axios
    .get(URL_API + "preguntas/", token)
    .then((response) => {
      if (response) {
        preguntas.value = response.data.preguntas.filter((pregunta)=> pregunta.estado === 1);
      }
    })
    .catch((error) => {
      console.log(error);
    });
};

const theaders = () => {
  const equipos_th = equipos.value.map((equipo) => ({
    name: equipo.nombre,
    field: equipo.nombre.toLowerCase(),
    sort: "",
    id: equipo.id,
  }));
  equipos_th.forEach((equipo) => cols.push(equipo));
};

const getData = () =>{
  getDataEquipo_Has_Pregunta();
  getPreguntas();
  getEquipos();
}

onBeforeMount(() => {
  getData();
});

const getIdEquipo_Has_Pregunta = (id_pregunta, id_equipo) => {
  const registroEncontrado = equipo_has_preguntas.value.find(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 1 &&
      registro.habilitado === 1
  );

  // Si encontramos el registro, retornamos su id
  // De lo contrario, podríamos retornar null, undefined o un valor indicativo según tu lógica de negocio
  return registroEncontrado ? registroEncontrado.id : null;
};
const getIdEquipo_Has_Pregunta2 = (id_pregunta, id_equipo) => {
  const registroEncontrado = equipo_has_preguntas.value.find(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 2 &&
      registro.habilitado === 1
  );

  // Si encontramos el registro, retornamos su id
  // De lo contrario, podríamos retornar null, undefined o un valor indicativo según tu lógica de negocio
  return registroEncontrado ? registroEncontrado.id : null;
};
const getIdEquipo_Has_Pregunta3 = (id_pregunta, id_equipo) => {
  const registroEncontrado = equipo_has_preguntas.value.find(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 3 &&
      registro.habilitado === 1
  );

  // Si encontramos el registro, retornamos su id
  // De lo contrario, podríamos retornar null, undefined o un valor indicativo según tu lógica de negocio
  return registroEncontrado ? registroEncontrado.id : null;
};

const isCheckedState1 = (id_pregunta, id_equipo) => {
  return equipo_has_preguntas.value.some(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 1 &&
      registro.habilitado === 1
  );
};
const isCheckedState2 = (id_pregunta, id_equipo) => {
  return equipo_has_preguntas.value.some(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 2 &&
      registro.habilitado === 1
  );
};
const isCheckedState3 = (id_pregunta, id_equipo) => {
  return equipo_has_preguntas.value.some(
    (registro) =>
      registro.id_pregunta === id_pregunta &&
      registro.id_equipo === id_equipo &&
      registro.estado === 3 &&
      registro.habilitado === 1
  );
};

const estado_equipo_has_pregunta = (idPregunta, idEquipo, event, id_equipo_has_pregunta) => {
  if (event.target.checked) {
    const equipo_has_pregunta = {
      id: id_equipo_has_pregunta,
      id_pregunta: idPregunta,
      id_equipo: idEquipo,
      estado: equipo_estado.value,
    };
    Swal.fire({
      showCancelButton: true,
      showConfirmButton: true,
      title: "¿Desea guardar un nuevo registro?",
      text: "Se registrara una pregunta a un equipo",
      icon: "question",
    }).then((result) => {
      if (result.isConfirmed) {
        axios
          .post(URL_API + "equipo_preguntas/", equipo_has_pregunta, token)
          .then((response) => {
            if (response) {
              getDataEquipo_Has_Pregunta();
              getPreguntas();
              getEquipos();
              Swal.fire("Guardado", "", "success");
            }
          })
          .catch((e) => console.log(e));
      } else if (result.isDismissed) {
        event.target.checked = false;
        Swal.fire("Cancelado", "", "success");
      }
    });
  } else {
    const equipo_has_pregunta = {
      id_equipo: idEquipo,
      id_pregunta: idPregunta,
      estado: equipo_estado.value,
      habilitado: 0,
    };
    Swal.fire({
      showCancelButton: true,
      showConfirmButton: true,
      title: "¿Desea deshailitar un registro?",
      text: "Se deshabilitara una pregunta a un equipo",
      icon: "question",
    }).then((result) => {
      if (result.isConfirmed) {
        axios
          .put(URL_API +"equipo_preguntas/" + event.target.getAttribute("id_equipo_has_pregunta"),equipo_has_pregunta, token
          )
          .then((response) => {
            if (response) {
              Swal.fire("Guardado", "", "success");
            }
          })
          .catch((e) => console.log(e));
      } else if (result.isDismissed) {
        event.target.checked = false;
        Swal.fire("Cancelado", "", "success");
      }
    });
  }
};

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

onUpdated(() => {
  getDataEquipo_Has_Pregunta();
  getPreguntas();
  getEquipos();
});

const pregunta_id = ref();

const changeEstadoModal = (id,row) => {
  //crear: 0
  //editar: 1
  console.log(row);
  switch(id) {
    case 0:
      estado_modal.value = 0;
      pregunta_modal.value = '';
      pregunta_id.value = null;
      break; // Añadir break
    case 1:
      estado_modal.value = 1
      pregunta_modal.value = row.descripcion;
      pregunta_id.value = row.id;
      break; // Añadir break
    // Añadir caso por defecto
    default:
      console.log('ID no válido');
  }
}

const eliminarPregunta = (id, estado) => {
  Swal.fire({
    title: "¿Estás seguro?",
    text: "Esta acción deshabilitará la pregunta a los equipos asociados",
    icon: "warning",
    showCancelButton: true,
    confirmButtonColor: "#45DABE",
    cancelButtonColor: "#1F2937",
    confirmButtonText: "Sí, deshabilitar",
    cancelButtonText: "Cancelar"
  }).then((result) => {
    if (result.isConfirmed) {
      axios.put(`${URL_API}equipo_preguntas/deshabilitar/${id}/${estado}`, {}, token)
        .then((response) => {
          if (response) {
            Swal.fire({
              title: "Preguntas deshabilitadas",
              icon: "success",
              confirmButtonColor: "#45DABE",
            });
          }
        })
        .catch((e) => {
          console.log(e);
          Swal.fire({
            title: "Error",
            text: "Hubo un problema al deshabilitar las preguntas del los equipos",
            icon: "error"
          });
        });

      getData();
    } else {
      Swal.fire({
        title: "Acción cancelada",
        text: "La pregunta no ha sido deshabilitada",
        icon: "info",
        confirmButtonColor: "#45DABE",
      });
    }
  });
};

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
  <!-- Page Content -->
  <div class="content">
    <button
        type="button"
        class="btn btn-dark col-1 offset-11 waves-effect waves-light"
        data-bs-toggle="modal"
        data-bs-target="#modal-block-small"
        @click="changeEstadoModal(0)"
        >
        Agregar
    </button>
    <ModalMantenedorPreguntas 
      :estado="estado_modal"
      :pregunta="pregunta_modal"
      :pregunta_id="pregunta_id"
      @getData="getData"
    />
    <BaseBlock content-full>
      <label for="equipo_estado">Estado del equipo: </label>
      <select
        class="form-select col-1"
        style="width: 140px"
        name="equipo_estado"
        id="equipo_estado"
        v-model="equipo_estado"
        @change="ver_estado_equipo"
      >
        <option value="1">Prendido</option>
        <option value="2">Apagado</option>
        <option value="3">Bloqueado</option>
      </select>
      <Dataset
        v-slot="{ ds }"
        :ds-data="preguntas"
        :ds-sortby="sortBy"
        :ds-search-in="['nombreBodega', 'creado']"
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
            <div class="table-responsive" v-if="equipo_estado == 1">
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
                  <template #default="{ row }">
                    <tr>
                      <td scope="row">{{ row.id}}</td>
                      <td>
                        <div class="btn-group">
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            data-bs-toggle="modal"
                            data-bs-target="#modal-block-small"
                            @click="changeEstadoModal(1 ,row)"
                          >
                            <i class="fa fa-fw fa-pencil-alt"></i>
                          </button>
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            @click="eliminarPregunta(row.id, 1)"
                          >
                            <i class="fa fa-fw fa-times"></i>
                          </button>
                        </div>
                      </td>
                      <td>{{ row.descripcion }}</td>
                      <td v-for="equipo in equipos" :key="equipo.id">
                        <input
                          class="form-check-input"
                          type="checkbox"
                          :id_pregunta="row.id"
                          :id_equipo="equipo.id"
                          :id_equipo_has_pregunta="getIdEquipo_Has_Pregunta(row.id, equipo.id)"
                          :checked="isCheckedState1(row.id, equipo.id, equipo_estado)"
                          @change="estado_equipo_has_pregunta(
                              row.id,
                              equipo.id,
                              $event
                            )
                          "
                        />
                      </td>
                    </tr>
                  </template>
                </DatasetItem>
              </table>
            </div>
            <div class="table-responsive" v-else-if="equipo_estado == 2">
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
                      {{ th.name + " " + th.id }}
                    </th>
                  </tr>
                </thead>
                <DatasetItem tag="tbody" class="fs-sm">
                  <template #default="{ row, rowIndex }">
                    <tr>
                      <td scope="row">{{ rowIndex + 1 }}</td>
                      <td>
                        <div class="btn-group">
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            data-bs-toggle="modal"
                            data-bs-target="#modal-block-small"
                            @click="changeEstadoModal(1, row)"
                          >
                            <i class="fa fa-fw fa-pencil-alt"></i>
                          </button>
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            @click="eliminarPregunta(row.id, 2)"
                          >
                            <i class="fa fa-fw fa-times"></i>
                          </button>
                        </div>
                      </td>
                      <td>{{ row.descripcion + " " + row.id }}</td>
                      <!--<td v-for="equipo in equipos">{{ equipo.nombre }}</td>-->
                      <td v-for="equipo in equipos" :key="equipo.id">
                        <input
                          class="form-check-input"
                          type="checkbox"
                          :id_pregunta="row.id"
                          :id_equipo="equipo.id"
                          :id_equipo_has_pregunta="
                            getIdEquipo_Has_Pregunta2(row.id, equipo.id)
                          "
                          :checked="
                            isCheckedState2(row.id, equipo.id, equipo_estado)
                          "
                          @change="
                            estado_equipo_has_pregunta(
                              row.id,
                              equipo.id,
                              $event
                            )
                          "
                        />
                      </td>
                    </tr>
                  </template>
                </DatasetItem>
              </table>
            </div>
            <div class="table-responsive" v-else-if="equipo_estado == 3">
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
                      {{ th.name + " " + th.id }}
                    </th>
                  </tr>
                </thead>
                <DatasetItem tag="tbody" class="fs-sm">
                  <template #default="{ row, rowIndex }">
                    <tr>
                      <td scope="row">{{ rowIndex + 1 }}</td>
                      <td>
                        <div class="btn-group">
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            data-bs-toggle="modal"
                            data-bs-target="#modal-block-small"
                            @click="changeEstadoModal(1, row)"
                          >
                            <i class="fa fa-fw fa-pencil-alt"></i>
                          </button>
                          <button
                            type="button"
                            class="btn btn-sm btn-alt-secondary"
                            @click="eliminarPregunta(row.id, 3)"
                          >
                            <i class="fa fa-fw fa-times"></i>
                          </button>
                        </div>
                      </td>
                      <td>{{ row.descripcion + " " + row.id }}</td>
                      <!--<td v-for="equipo in equipos">{{ equipo.nombre }}</td>-->
                      <td v-for="equipo in equipos" :key="equipo.id">
                        <input
                          class="form-check-input"
                          type="checkbox"
                          :id_pregunta="row.id"
                          :id_equipo="equipo.id"
                          :id_equipo_has_pregunta="
                            getIdEquipo_Has_Pregunta3(row.id, equipo.id)
                          "
                          :checked="isCheckedState3(row.id, equipo.id)"
                          @change="
                            estado_equipo_has_pregunta(
                              row.id,
                              equipo.id,
                              $event
                            )
                          "
                        />
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
