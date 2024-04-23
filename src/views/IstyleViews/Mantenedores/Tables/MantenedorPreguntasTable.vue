<script setup>
import { reactive, computed, onMounted } from "vue";

// Vue Dataset, for more info and examples you can check out https://github.com/kouts/vue-dataset/tree/next
import {
  Dataset,
  DatasetItem,
  DatasetInfo,
  DatasetPager,
  DatasetSearch,
  DatasetShow,
} from "vue-dataset";

// Get example data
import users from "@/data/usersDataset.json";
import ModalMantenedorPreguntas from '../Modals/ModalMantenedorPreguntas.vue';
// Helper variables
const cols = reactive([
  {
    name: "Acciones",
    field: "pregunta",
    sort: "",
  },
  {
    name: "Preguntas",
    field: "pregunta",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
    sort: "",
  },
  {
    name: "equipo",
    field: "equipo",
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
</script>

<style lang="scss" scoped>

th{
  background-color: #45DABE;
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
    <ModalMantenedorPreguntas/>
    <BaseBlock content-full>
      <Dataset
        v-slot="{ ds }"
        :ds-data="users"
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
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <i class="fa fa-fw fa-pencil-alt"></i>
                          </button>
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <i class="fa fa-fw fa-times"></i>
                          </button>
                        </div>
                      </td>
                      <td >{{ row.name }}</td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
                          </button>
                        </div>
                      </td>
                      <td >
                        <div class="btn-group">
                          <button type="button" class="btn btn-sm btn-alt-secondary">
                            <input type="checkbox"/>
                          </button>
                          <button type="button" class="btn btn-sm btn-success">
                            <i class="fa-solid fa-circle-plus"></i>
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
