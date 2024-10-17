<script setup>
import { watch, ref } from 'vue';

const props = defineProps(["getPreguntas"]);
const emit = defineEmits(["custom-change", "text-change"]);

function cargarChecks(e) {
  emit("custom-change", { id: e.target.value, checked: e.target.checked });
}
function cargartextos(id) {
  let texto = document.getElementById(id).value;
  emit("text-change", { id, texto });
}

const nuevaPregunta = ref();

watch(() => props.getPreguntas, (newPregunta) => {
  nuevaPregunta.value = newPregunta || '';
  console.log("Desde form", nuevaPregunta.value);
}, { immediate: true });

</script>

<template>
  <div class="row mt-5">
    <!-- Columna 1 -->
    <div
      class="col-md-6"
      v-for="preguntas in props.getPreguntas"
      :key="preguntas.id"
    >
      <div class="row">
        <div class="col-6 form-group">
          <p>
            {{
              preguntas.pregunta.descripcion || "Sin Datos para este Equipo."
            }}
          </p>
        </div>
        <div class="col-6 form-group">
          <div class="row">
            <div class="col-4 form-check form-switch">
              <input
                class="form-check-input"
                type="checkbox"
                :value="preguntas.pregunta.id"
                @change="cargarChecks"
                checked="true"
              />
            </div>
            <div class="col-8">
              <input
                type="text"
                class="form-control form-control-sm"
                :id="preguntas.id"
                @keyup="cargartextos(preguntas.id)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>
