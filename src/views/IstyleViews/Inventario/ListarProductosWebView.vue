<script setup></script>

<template>
  <section id="column-selectors">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-header">
            <h4 class="card-title">Productos Web</h4>
          </div>
          <div class="card-content">
            <div class="card-body card-dashboard">
              <div class="table-responsive">
                <div class="mt-4">
                  <div class="VueTables VueTables--client">
                    <div class="row">
                      <div class="col-md-12">
                        <div
                          class="form-group form-inline pull-left VueTables__search"
                        >
                          <div class="VueTables__search-field">
                            <label for="VueTables__search_Lnb9M" class=""
                              >Busqueda:</label
                            ><input
                              type="text"
                              placeholder="Registro a Buscar"
                              id="VueTables__search_Lnb9M"
                              autocomplete="off"
                              class="VueTables__search__input form-control"
                            />
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="table-responsive">
                      <table
                        class="VueTables__table table table-striped table-bordered table-hover"
                        style="overflow: hidden"
                      >
                        <thead>
                          <tr>
                            <th
                              title=""
                              tabindex="0"
                              class="VueTables__sortable"
                              style="position: relative"
                            >
                              <span class="VueTables__heading">id</span
                              ><span
                                class="VueTables__sort-icon pull-right glyphicon glyphicon-sort"
                              ></span>
                              <div
                                class="resize-handle"
                                style="
                                  top: 0px;
                                  right: 0px;
                                  width: 5px;
                                  position: absolute;
                                  cursor: col-resize;
                                  user-select: none;
                                  height: 94px;
                                "
                              ></div>
                            </th>
                            <th
                              title=""
                              tabindex="0"
                              class="VueTables__sortable"
                              style="position: relative"
                            >
                              <span class="VueTables__heading">Nombre</span
                              ><span
                                class="VueTables__sort-icon pull-right glyphicon glyphicon-sort"
                              ></span>
                              <div
                                class="resize-handle"
                                style="
                                  top: 0px;
                                  right: 0px;
                                  width: 5px;
                                  position: absolute;
                                  cursor: col-resize;
                                  user-select: none;
                                  height: 94px;
                                "
                              ></div>
                            </th>
                            <th
                              title=""
                              tabindex="0"
                              class=""
                              style="position: relative"
                            >
                              <span class="VueTables__heading">Stock</span>
                              <div
                                class="resize-handle"
                                style="
                                  top: 0px;
                                  right: 0px;
                                  width: 5px;
                                  position: absolute;
                                  cursor: col-resize;
                                  user-select: none;
                                  height: 94px;
                                "
                              ></div>
                            </th>
                            <th
                              title=""
                              tabindex="0"
                              class=""
                              style="position: relative"
                            >
                              <span class="VueTables__heading">Precio</span>
                              <div
                                class="resize-handle"
                                style="
                                  top: 0px;
                                  right: 0px;
                                  width: 5px;
                                  position: absolute;
                                  cursor: col-resize;
                                  user-select: none;
                                  height: 94px;
                                "
                              ></div>
                            </th>
                            <th
                              title=""
                              tabindex="0"
                              class=""
                              style="position: relative"
                            >
                              <span class="VueTables__heading">Eliminar</span>
                              <div
                                class="resize-handle"
                                style="
                                  top: 0px;
                                  right: 0px;
                                  width: 5px;
                                  position: absolute;
                                  cursor: col-resize;
                                  user-select: none;
                                  height: 94px;
                                "
                              ></div>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr class="VueTables__no-results">
                            <td tabindex="0" colspan="5" class="text-center">
                              No hay registros coincidentes
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                    <div class="VuePagination row col-md-12">
                      <nav class="text-center">
                        <ul
                          class="pagination VuePagination__pagination"
                          style="display: none"
                        >
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-prev-chunk disabled"
                          >
                            <a
                              href="javascript:void(0);"
                              disabled="disabled"
                              class="page-link"
                              >&lt;&lt;</a
                            >
                          </li>
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-prev-page disabled"
                          >
                            <a
                              href="javascript:void(0);"
                              disabled="disabled"
                              class="page-link"
                              >&lt;</a
                            >
                          </li>
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-next-page disabled"
                          >
                            <a
                              href="javascript:void(0);"
                              disabled="disabled"
                              class="page-link"
                              >&gt;</a
                            >
                          </li>
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-next-chunk disabled"
                          >
                            <a
                              href="javascript:void(0);"
                              disabled="disabled"
                              class="page-link"
                              >&gt;&gt;</a
                            >
                          </li>
                        </ul>
                        <p
                          class="VuePagination__count text-center col-md-12"
                          style="display: none"
                        >
                          0 registros
                        </p>
                      </nav>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
