<script setup>
import { reactive, computed } from "vue";
import { useRouter } from "vue-router";
import { useTemplateStore } from "@/stores/template";

// Vuelidate, for more info and examples you can check out https://github.com/vuelidate/vuelidate
import useVuelidate from "@vuelidate/core";
import { required, minLength } from "@vuelidate/validators";

// Main store and Router
const store = useTemplateStore();
const router = useRouter();

// Input state variables
const state = reactive({
  username: null,
  password: null,
});

// Validation rules
const rules = computed(() => {
  return {
    username: {
      required,
      minLength: minLength(3),
    },
    password: {
      required,
      minLength: minLength(5),
    },
  };
});

// Use vuelidate
const v$ = useVuelidate(rules, state);

// On form submission
async function onSubmit() {
  const result = await v$.value.$validate();

  if (!result) {
    // notify user form is invalid
    return;
  }

  // Go to dashboard
  router.push({ name: "backend-pages-auth" });
}
</script>

<template>
  <!-- Page Content -->
  <!--Foto lateral en el login-->
  <BaseBackground image="/assets/media/istyle/fondo_login.png">
    <div class="row g-0">
      <!-- Meta Info Section -->
      <div
        class="hero-static col-lg-4 d-none d-lg-flex flex-column justify-content-center"
      >
  
        <div
          class="p-4 p-xl-5 d-xl-flex justify-content-between align-items-center fs-sm"
        >
          
        </div>
      </div>
      <!-- END Meta Info Section -->

      <!-- Main Section -->
      <div class="hero-static col-lg-8 d-flex flex-column align-items-center">
        <div class="p-4 flex-grow-1 d-flex align-items-center">
          <!-- Contenedor principal del logo y formulario -->
          <div style="position: relative">
            <img
              src="/public/assets/media/istyle/isote separado-03.png"
              class="imgFondo"
            />
            <!-- Header -->
            <div class="text-center mb-3">
              <!--   Logo  -->
              <img src="/public/assets/media/istyle/logoIstyle.png" class="imgLgo" />
            </div>
            <!-- END Header -->

            <!-- Sign In Form -->
            <div class="row g-0 justify-content-center bg">
              <div class="col-sm-8 col-xl-4">
                <form @submit.prevent="onSubmit" class="form-overlay">
                  <div class="mb-4">
                    <input
                      type="text"
                      class="form-control"
                      id="login-username"
                      name="login-username"
                      placeholder="Username"
                      :class="{
                        'is-invalid': v$.username.$errors.length,
                      }"
                      v-model="state.username"
                      @blur="v$.username.$touch"
                    />
                    <div
                      v-if="v$.username.$errors.length"
                      class="invalid-feedback animated fadeIn"
                    >
                      Please enter your username
                    </div>
                  </div>
                  <div class="mb-4">
                    <input
                      type="password"
                      class="form-control"
                      id="login-password"
                      name="login-password"
                      placeholder="Password"
                      :class="{
                        'is-invalid': v$.password.$errors.length,
                      }"
                      v-model="state.password"
                      @blur="v$.password.$touch"
                    />
                    <div
                      v-if="v$.password.$errors.length"
                      class="invalid-feedback animated fadeIn"
                    >
                      Please enter your password
                    </div>
                  </div>
                  <div
                    class="d-flex justify-content-center align-items-center mb-4"
                  >
                    <div>
                      <button type="submit" class="btn btn-info">
                        <i class="fa fa-fw fa-sign-in-alt me-1 "></i>
                        Login
                      </button>
                    </div>
                  </div>
                </form>
              </div>
            </div>
            <!-- END Sign In Form -->
          </div>
        </div>
      </div>
      <!-- END Main Section -->
    </div>
  </BaseBackground>
  <!-- END Page Content -->
</template>

<style>
.imgLgo {
  width: 50%;
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  border-radius: 10px;
}
.form-overlay {
  position: absolute;
  top: 60%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  border-radius: 10px;
}
.imgFondo {
  width: 80%;
  margin-left: 10%;
}
</style>
