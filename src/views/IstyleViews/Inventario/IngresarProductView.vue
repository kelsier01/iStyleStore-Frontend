<script setup></script>

<template>
  <section id="column-selectors">
    <div class="row">
      <div class="col-12">
        <div class="card">
          <div class="card-header"><h4 class="card-title">Productos</h4></div>
          <div class="card-content">
            <div class="card-body card-dashboard">
              <div class="text-center">
                <button class="btn btn-primary waves-effect waves-light">
                  <span class="feather icon-file-plus"></span> Nuevo Producto
                </button>
              </div>
              <div class="table-responsive">
                <div class="mt-4">
                  <div class="VueTables VueTables--client">
                    <div class="row">
                      <div class="col-md-12">
                        <div
                          class="form-group form-inline pull-left VueTables__search"
                        >
                          <div class="VueTables__search-field">
                            <label for="VueTables__search_BjQ2H" class=""
                              >Busqueda:</label
                            ><input
                              type="text"
                              placeholder="Registro a Buscar"
                              id="VueTables__search_BjQ2H"
                              autocomplete="off"
                              class="VueTables__search__input form-control"
                            />
                          </div>
                        </div>
                        <div
                          class="form-group form-inline pull-right VueTables__limit"
                        >
                          <div class="VueTables__limit-field">
                            <label for="VueTables__limit_BjQ2H"
                              >Limite de registros:</label
                            ><select
                              id="VueTables__limit_BjQ2H"
                              class="form-control"
                            >
                              <option value="10">10</option>
                              <option value="25">25</option>
                              <option value="50">50</option>
                              <option value="100">100</option>
                            </select>
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
                              <span class="VueTables__heading">Codigo</span
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
                              class="VueTables__sortable"
                              style="position: relative"
                            >
                              <span class="VueTables__heading">Stock</span
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
                              <span class="VueTables__heading">Precio</span
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
                              <span class="VueTables__heading">Categoria</span
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
                              <span class="VueTables__heading">Marca</span
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
                              <span class="VueTables__heading"
                                >Agregar Stock</span
                              >
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
                              <span class="VueTables__heading"
                                >Cambio Bodega</span
                              >
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
                              <span class="VueTables__heading">Editar</span>
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
                              <span class="VueTables__heading">Imprimir</span>
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
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">89cc14862c</td>
                            <td tabindex="0" class="">
                              AUDIFONOS TREKZ TITANIUM AZUL
                            </td>
                            <td tabindex="0" class="">2</td>
                            <td tabindex="0" class="">149990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">AFTERSHOKZ</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">7b7542122c</td>
                            <td tabindex="0" class="">prueba 2 alejandro</td>
                            <td tabindex="0" class="">109</td>
                            <td tabindex="0" class="">2767570</td>
                            <td tabindex="0" class="">iphone</td>
                            <td tabindex="0" class="">AFTERSHOKZ</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">0674a318d5</td>
                            <td tabindex="0" class="">hhkkh</td>
                            <td tabindex="0" class="">20</td>
                            <td tabindex="0" class="">169618</td>
                            <td tabindex="0" class="">iphone</td>
                            <td tabindex="0" class="">AFTERSHOKZ</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">087eb1b2dc</td>
                            <td tabindex="0" class="">hhkkh2536</td>
                            <td tabindex="0" class="">10</td>
                            <td tabindex="0" class="">169618</td>
                            <td tabindex="0" class="">iphone</td>
                            <td tabindex="0" class="">ILUV</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">dd4bea2543</td>
                            <td tabindex="0" class="">gdgffgfg</td>
                            <td tabindex="0" class="">10</td>
                            <td tabindex="0" class="">169618</td>
                            <td tabindex="0" class="">iphone</td>
                            <td tabindex="0" class="">SAMSUNG</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">d0297e236d</td>
                            <td tabindex="0" class="">PRUEBA ISTYLE 4</td>
                            <td tabindex="0" class="">15</td>
                            <td tabindex="0" class="">47600</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">HUAWEI</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">51c7c6ad26</td>
                            <td tabindex="0" class="">PRUEBA 5</td>
                            <td tabindex="0" class="">4</td>
                            <td tabindex="0" class="">19990</td>
                            <td tabindex="0" class="">LÁMINAS</td>
                            <td tabindex="0" class="">PUREGEAR</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">e6d163e820</td>
                            <td tabindex="0" class="">
                              AUDIFONOS TREKZ TITANIUM NEGRO
                            </td>
                            <td tabindex="0" class="">2</td>
                            <td tabindex="0" class="">149990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">AFTERSHOKZ</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">0a82652dca</td>
                            <td tabindex="0" class="">
                              AUDIFONOS TREKZ AIR NEGRO
                            </td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">99990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">AFTERSHOKZ</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">c99bff6710</td>
                            <td tabindex="0" class="">
                              PARLANTE SOUND CORE SPORT XL
                            </td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">59990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">ANKER</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">b97fc2af39</td>
                            <td tabindex="0" class="">
                              PARLANTE SOUND CORE SPORT
                            </td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">59990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">ANKER</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">b525ffdc56</td>
                            <td tabindex="0" class="">
                              AUDIFONOS EAR PODS LIGHTNING CONNECTOR
                            </td>
                            <td tabindex="0" class="">9</td>
                            <td tabindex="0" class="">32990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">APPLE</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">bd1f8f2ff3</td>
                            <td tabindex="0" class="">
                              AUDIFONOS EAR PODS HEADPHONE PLUG
                            </td>
                            <td tabindex="0" class="">14</td>
                            <td tabindex="0" class="">29990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">APPLE</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">5bade97baf</td>
                            <td tabindex="0" class="">
                              AUDIFONOS EAR PODS LIGHTNING CONNECTOR BULK
                            </td>
                            <td tabindex="0" class="">20</td>
                            <td tabindex="0" class="">29990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">APPLE</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">42636b55fb</td>
                            <td tabindex="0" class="">PARLANTE ZERO CHILL</td>
                            <td tabindex="0" class="">2</td>
                            <td tabindex="0" class="">59990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JAM</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">d2299f6d23</td>
                            <td tabindex="0" class="">PARLANTE HANG UP</td>
                            <td tabindex="0" class="">2</td>
                            <td tabindex="0" class="">39990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JAM</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">8ffabdffc4</td>
                            <td tabindex="0" class="">
                              PARLANTE LIVE FAST AZUL
                            </td>
                            <td tabindex="0" class="">3</td>
                            <td tabindex="0" class="">36990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JAM</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">e6106a3b84</td>
                            <td tabindex="0" class="">PARLANTE LIVE LOOSE</td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">26990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JAM</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">9a5c74d079</td>
                            <td tabindex="0" class="">PARLANTE DOUBLE CHILL</td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">49990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JAM</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">5886680cb9</td>
                            <td tabindex="0" class="">AUDIFONOS EVEREST 310</td>
                            <td tabindex="0" class="">2</td>
                            <td tabindex="0" class="">189990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JBL</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">c7d8b9aacd</td>
                            <td tabindex="0" class="">PARLANTE CHARGE 3</td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">99990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JBL</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">43881c655f</td>
                            <td tabindex="0" class="">PARLANTE CLIP 2</td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">49990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JBL</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">5f5a3bf3ec</td>
                            <td tabindex="0" class="">
                              AUDIFONOS REFLECT AWARE
                            </td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">129990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JBL</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">15b6153677</td>
                            <td tabindex="0" class="">PARLANTE FLIP 4</td>
                            <td tabindex="0" class="">1</td>
                            <td tabindex="0" class="">79990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">JBL</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                          <tr class="VueTables__row">
                            <td tabindex="0" class="">f2b4fdd6f0</td>
                            <td tabindex="0" class="">
                              AUDIFONOS POSITIVE VIBRATION 2
                            </td>
                            <td tabindex="0" class="">8</td>
                            <td tabindex="0" class="">49990</td>
                            <td tabindex="0" class="">AUDIFONOS Y PARLANTES</td>
                            <td tabindex="0" class="">MARLEY</td>
                            <td tabindex="0" class="">
                              <a class="feather icon-file-plus"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-chevrons-right"></a>
                            </td>
                            <td tabindex="0" class="">
                              <a
                                data-toggle="modal"
                                data-target="#xlarge"
                                class="feather icon-edit-2"
                              ></a>
                            </td>
                            <td tabindex="0" class="">
                              <a class="feather icon-printer"></a>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                    <div class="VuePagination row col-md-12">
                      <nav class="text-center">
                        <ul
                          class="pagination VuePagination__pagination"
                          style=""
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
                            class="VuePagination__pagination-item page-item active"
                          >
                            <a
                              href="javascript:void(0)"
                              class="page-link active"
                              role="button"
                              >1</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              class="page-link"
                              role="button"
                              >2</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >3</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >4</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >5</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >6</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >7</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >8</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >9</a
                            >
                          </li>
                          <li class="VuePagination__pagination-item page-item">
                            <a
                              href="javascript:void(0)"
                              role="button"
                              class="page-link"
                              >10</a
                            >
                          </li>
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-next-page"
                          >
                            <a href="javascript:void(0);" class="page-link"
                              >&gt;</a
                            >
                          </li>
                          <li
                            class="VuePagination__pagination-item page-item VuePagination__pagination-item-next-chunk"
                          >
                            <a href="javascript:void(0);" class="page-link"
                              >&gt;&gt;</a
                            >
                          </li>
                        </ul>
                        <p
                          class="VuePagination__count text-center col-md-12"
                          style=""
                        >
                          Mostrando 1 a 25 de 350 registros
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
