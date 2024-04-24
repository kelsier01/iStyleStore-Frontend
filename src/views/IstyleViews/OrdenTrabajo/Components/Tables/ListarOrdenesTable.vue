<script setup>
import { reactive, computed, onMounted } from "vue";
import { RouterLink } from 'vue-router'
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

// Helper variables
const cols = reactive([
  {
    name: "Cliente",
    field: "name",
    sort: "",
  },
  {
    name: "Equipo",
    field: "email",
    sort: "",
  },
  {
    name: "Modelo",
    field: "company",
    sort: "",
  },
  {
    name: "Observacion",
    field: "birthdate",
    sort: "",
  },
  {
    name: "Fecha de Venta",
    field: "birthdate",
    sort: "",
  },
  {
    name: "Agregar Nota",
    field: "birthdate",
    sort: "",
  },
  {
    name: "Revision",
    field: "birthdate",
    sort: "",
  },
  {
    name: "Ot",
    field: "birthdate",
    sort: "",
  },
  {
    name: "Eliminar",
    field: "birthdate",
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
    <BaseBlock content-full>
      <Dataset
        v-slot="{ ds }"
        :ds-data="users"
        :ds-sortby="sortBy"
        :ds-search-in="['name', 'email', 'company', 'birthdate']"
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
                    <th scope="col">ID</th>
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
                      <td >{{ row.name }}</td>
                      <td>{{ row.name }}</td>
                      <td >{{ row.company }}</td>
                      <td >{{ row.birthdate }}</td>
                      <td >{{ row.name }}</td>
                      <td ><i class="fa-solid fa-square-phone"></i></td>
                      <td>
                        <router-link to='/ordenpdf'>
                            <i class="fa-solid fa-file-pdf"></i>
                        </router-link>
                      </td>
                      <td>
                        <router-link to='/ordenprotocolo'>
                          <i class="fa-solid fa-file-pdf"></i>
                        </router-link>
                      </td>
                      <td >
                          <i class="fa fa-trash"></i>
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
