<script setup>
    
</script>

<template>
    <button
        type="button"
        class="btn btn-dark col-1 offset-11 waves-effect waves-light"
        data-bs-toggle="modal"
        data-bs-target="#modal-block-small"
        >
        Agregar
    </button>
    
    <!-- Small Block Modal -->
    <div
      class="modal"
      id="modal-block-small"
      tabindex="-1"
      role="dialog"
      aria-labelledby="modal-block-small"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-dialog-centered modal-sm" role="document">
        <div class="modal-content">
          <BaseBlock title="Agregar Preguntas" transparent class="mb-0">
            <template #options>
              <button
                type="button"
                class="btn-block-option"
                data-bs-dismiss="modal"
                aria-label="Close"
              >
                <i class="fa fa-fw fa-times"></i>
              </button>
            </template>

            <template #content>
              <div class="block-content fs-sm">
                <div class="form-group">
                  <label for="modal-block-small-name">Ingresar pregunta:</label>
                  <input
                    type="text"
                    class="form-control mb-3 mt-3"
                    id="modal-block-small-name"
                    name="modal-block-small-name"
                  />
                </div>
              </div>
              <div class="block-content block-content-full text-end bg-body">
                <button
                  type="button"
                  class="btn btn-sm btn-alt-secondary me-1"
                  data-bs-dismiss="modal"
                >
                  Cerrar
                </button>
                <button
                  type="button"
                  class="btn btn-sm btn-dark"
                  data-bs-dismiss="modal"
                >
                  Guardar
                </button>
              </div>
            </template>
          </BaseBlock>
        </div>
      </div>
    </div>
    <!-- END Small Block Modal -->
</template>

<style>
    
</style>