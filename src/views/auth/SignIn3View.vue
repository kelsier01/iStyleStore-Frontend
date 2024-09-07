<script setup>
import { reactive, computed } from "vue";
import { useRouter, RouterLink } from "vue-router";
import axios from "axios";
import Swal from "sweetalert2";

// Vuelidate, for more info and examples you can check out https://github.com/vuelidate/vuelidate
import useVuelidate from "@vuelidate/core";
import { required, minLength } from "@vuelidate/validators";

// Main store and Router
const router = useRouter();
const rutaAPI = import.meta.env.VITE_URL_API;
// Input state variables
const state = reactive({
  email: null,
  password: null,
});

// Validation rules
const rules = computed(() => {
  return {
    email: {
      required,
      minLength: minLength(3),
    },
    password: {
      required,
      minLength: minLength(4),
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
  axios
    .post(rutaAPI + "auth/login", state)
    .then(function (response) {
      // handle success
      localStorage.setItem("Nombre", response.data.user.name);
      localStorage.setItem("Token", response.data.token);
      router.push({ name: "backend-dashboard" });
      console.log(response);
    })
    .catch(function (error) {
      // handle error
      Swal.fire({
        title: "Error!",
        text: error.response.data.msg,
        icon: "error",
        confirmButtonText: "OK",
      });
    });
  // Go to dashboard
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
        ></div>
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
              <img
                src="/public/assets/media/istyle/logoIstyle.png"
                class="imgLgo"
              />
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
                      id="login-email"
                      name="login-email"
                      placeholder="email"
                      :class="{
                        'is-invalid': v$.email.$errors.length,
                      }"
                      v-model="state.email"
                      @blur="v$.email.$touch"
                    />
                    <div
                      v-if="v$.email.$errors.length"
                      class="invalid-feedback animated fadeIn"
                    >
                      Por favor, ingrese su correo
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
                      Por favor, ingrese una contraseña
                    </div>
                  </div>
                  <div
                    class="d-flex justify-content-center align-items-center mb-4"
                  >
                    <div>
                      <!-- Boton Login -->
                      <!-- <button type="submit" class="btn btn-info">
                        <i class="fa fa-fw fa-sign-in-alt me-1 "></i>
                        Login
                      </button> -->
                      <RouterLink to="" @click="onSubmit()" class="btn">
                        <img
                          class="mb-4"
                          src="/public/assets/media/istyle/btnL.png"
                          alt="branding logo"
                        />
                      </RouterLink>
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
.form-control {
  border-radius: 50px;
  font-size: 1.4rem !important;
  padding-left: 1.3rem !important;
}
</style>
