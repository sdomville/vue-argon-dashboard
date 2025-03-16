<script setup>
import { useStore } from "vuex";
const store = useStore();
const minimizeSidebar = () => store.commit("sidebarMinimize");

</script>
<template>
  <nav
    class="navbar navbar-main navbar-expand-lg px-0 mx-4 shadow-none border-radius-sm"
    v-bind="$attrs"
    id="navbarBlur"
    data-scroll="true"
  >
    <div class="px-3 py-1 container-fluid">
      <!-- <breadcrumbs
        :current-page="currentRouteName"
        :current-directory="currentDirectory"
      /> -->
    <h6
      class="mb-0 font-weight-bolder brand"
      :class="isNavFixed ? 'text-dark' : 'text-white'"
    >
    Alert Test Framework
    </h6>
      <div
        class="mt-2 collapse navbar-collapse mt-sm-0 me-md-0 me-sm-4"
        :class="'me-sm-4'"
        id="navbar"
      >
        <ul class="navbar-nav justify-content-end">
          <li class="nav-item d-xl-none ps-3 d-flex align-items-center">
            <a
              href="#"
              @click="minimizeSidebar"
              class="p-0 nav-link text-white"
              id="iconNavbarSidenav"
            >
              <div class="sidenav-toggler-inner">
                <i class="sidenav-toggler-line bg-white"></i>
                <i class="sidenav-toggler-line bg-white"></i>
                <i class="sidenav-toggler-line bg-white"></i>
              </div>
            </a>
          </li>

        </ul>
      </div>
    </div>
  </nav>
</template>
<style>
.brand {
  margin-top: 1.0em;
}
</style>
