<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import { useRouter } from "vue-router";
import { useTemplateStore } from "@/stores/template";

// Grab example data
import notifications from "@/data/notifications";

// Main store and Router
const store = useTemplateStore();
const router = useRouter();

// Reactive variables
const baseSearchTerm = ref("");

// On form search submit functionality
function onSubmitSearch() {
  router.push("/backend/pages/generic/search?" + baseSearchTerm.value);
}

// When ESCAPE key is hit close the header search section
function eventHeaderSearch(event) {
  if (event.which === 27) {
    event.preventDefault();
    store.headerSearch({ mode: "off" });
  }
}

// Attach ESCAPE key event listener
onMounted(() => {
  document.addEventListener("keydown", eventHeaderSearch);
});

// Remove keydown event listener
onUnmounted(() => {
  document.removeEventListener("keydown", eventHeaderSearch);
});
</script>

<template>
  <!-- Header -->
  <header id="page-header">
    <slot>
      <!-- Header Content -->
      <div class="content-header">
        <slot name="content">
          <!-- Left Section -->
          <div class="d-flex align-items-center">
            <slot name="content-left">
              <!-- Toggle Sidebar -->
              <button
                type="button"
                class="btn btn-sm btn-alt-secondary me-2 d-lg-none"
                @click="store.sidebar({ mode: 'toggle' })"
              >
                <i class="fa fa-fw fa-bars"></i>
              </button>
              <!-- END Toggle Sidebar -->

              <!-- Toggle Mini Sidebar -->
              <button
                type="button"
                class="btn btn-sm btn-dark me-2 d-none d-lg-inline-block"
                @click="store.sidebarMini({ mode: 'toggle' })"
              >
                <i class="fa fa-fw fa-ellipsis-v"></i>
              </button>
              <!-- END Toggle Mini Sidebar -->

              <!-- Open Search Section (visible on smaller screens) -->
              <button
                type="button"
                class="btn btn-sm btn-alt-secondary d-md-none"
                @click="store.headerSearch({ mode: 'on' })"
              >
                <i class="fa fa-fw fa-search"></i>
              </button>
              <!-- END Open Search Section -->

              <!-- Search Form (visible on larger screens) -->
              
              <!-- END Search Form -->
            </slot>
          </div>
          <!-- END Left Section -->

          <!-- Right Section -->
          <div class="d-flex align-items-center">
            <slot name="content-right">
              <!-- User Dropdown -->
              <div class="dropdown d-inline-block ms-2">
                <button
                  type="button"
                  class="btn btn-sm btn-dark d-flex align-items-center"
                  id="page-header-user-dropdown"
                  data-bs-toggle="dropdown"
                  aria-haspopup="true"
                  aria-expanded="false"
                >
                  <img
                    class="rounded-circle"
                    src="/assets/media/avatars/avatar10.jpg"
                    alt="Header Avatar"
                    style="width: 21px"
                  />
                  <span class="d-none d-sm-inline-block ms-2">John</span>
                  <i
                    class="fa fa-fw fa-angle-down d-none d-sm-inline-block opacity-50 ms-1 mt-1"
                  ></i>
                </button>
                <div
                  class="dropdown-menu dropdown-menu-md dropdown-menu-end p-0 border-0"
                  aria-labelledby="page-header-user-dropdown"
                >
                  <div
                    class="p-3 text-center bg-body-light border-bottom rounded-top"
                  >
                    <img
                      class="img-avatar img-avatar48 img-avatar-thumb"
                      src="/assets/media/avatars/avatar10.jpg"
                      alt="Header Avatar"
                    />
                    <p class="mt-2 mb-0 fw-medium">John Smith</p>
                    <p class="mb-0 text-muted fs-sm fw-medium">Web Developer</p>
                  </div>
                  <div class="p-2">
                  <!--
                    <a
                      class="dropdown-item d-flex align-items-center justify-content-between"
                      href="javascript:void(0)"
                    >
                      <span class="fs-sm fw-medium">Inbox</span>
                      <span class="badge rounded-pill bg-primary ms-2">3</span>
                    </a>
                    <RouterLink
                      :to="{ name: 'backend-pages-generic-profile' }"
                      class="dropdown-item d-flex align-items-center justify-content-between"
                    >
                      <span class="fs-sm fw-medium">Profile</span>
                      <span class="badge rounded-pill bg-primary ms-2">1</span>
                    </RouterLink>
                    <a
                      class="dropdown-item d-flex align-items-center justify-content-between"
                      href="javascript:void(0)"
                    >
                      <span class="fs-sm fw-medium">Settings</span>
                    </a>
                  </div>
                  <div role="separator" class="dropdown-divider m-0"></div>
                  <div class="p-2">
                    <RouterLink
                      :to="{ name: 'auth-lock' }"
                      class="dropdown-item d-flex align-items-center justify-content-between"
                    >
                      <span class="fs-sm fw-medium">Lock Account</span>
                    </RouterLink> -->
                    <RouterLink
                      :to="{ name: 'auth-signin' }"
                      class="dropdown-item d-flex align-items-center justify-content-between"
                    >
                      <span class="fs-sm fw-medium">Log Out</span>
                    </RouterLink>
                  </div>
                </div>
              </div>
              <!-- END User Dropdown -->

              <!-- Notifications Dropdown -->

              <!-- END Notifications Dropdown -->

              <!-- Toggle Side Overlay -->
              <!-- END Toggle Side Overlay -->
            </slot>
          </div>
          <!-- END Right Section -->
        </slot>
      </div>
      <!-- END Header Content -->

      <!-- Header Search -->
      <div
        id="page-header-search"
        class="overlay-header bg-body-extra-light"
        :class="{ show: store.settings.headerSearch }"
      >
        <div class="content-header">
          <form class="w-100" @submit.prevent="onSubmitSearch">
            <div class="input-group">
              <button
                type="button"
                class="btn btn-alt-danger"
                @click="store.headerSearch({ mode: 'off' })"
              >
                <i class="fa fa-fw fa-times-circle"></i>
              </button>
              <input
                type="text"
                class="form-control"
                placeholder="Search or hit ESC.."
                id="page-header-search-input"
                name="page-header-search-input"
                v-model="baseSearchTerm"
              />
            </div>
          </form>
        </div>
      </div>
      <!-- END Header Search -->

      <!-- Header Loader -->
      <div
        id="page-header-loader"
        class="overlay-header bg-body-extra-light"
        :class="{ show: store.settings.headerLoader }"
      >
        <div class="content-header">
          <div class="w-100 text-center">
            <i class="fa fa-fw fa-circle-notch fa-spin"></i>
          </div>
        </div>
      </div>
      <!-- END Header Loader -->
    </slot>
  </header>
  <!-- END Header -->
</template>
