<script setup>
import { computed } from "vue";
import { useStore } from "vuex";
import SidenavList from "./SidenavList.vue";
//import logo from "@/assets/img/logo-ct-dark.png";
//import logoWhite from "@/assets/img/logo-ct.png";
import buddyimg from "@/assets/img/buddy.png";

const store = useStore();
const isRTL = computed(() => store.state.isRTL);
const layout = computed(() => store.state.layout);
const sidebarType = computed(() => store.state.sidebarType);
const darkMode = computed(() => store.state.darkMode);
</script>
<template>
  <div
    v-show="layout === 'default'"
    class="min-height-300 position-absolute w-100"
    :class="`${darkMode ? 'bg-transparent' : 'bg-primary'}`"
  />

  <aside
    class="my-3 overflow-auto border-0 sidenav navbar navbar-vertical navbar-expand-xs border-radius-sm"
    :class="`${isRTL ? 'me-3 rotate-caret fixed-end' : 'fixed-start ms-3'}    
      ${
        layout === 'landing' ? 'bg-transparent shadow-none' : ' '
      } ${sidebarType}`"
    id="sidenav-main"
  >
    <div class="sidenav-header">
      <i
        class="top-0 p-3 cursor-pointer fas fa-times text-secondary opacity-5 position-absolute end-0 d-none d-xl-none"
        aria-hidden="true"
        id="iconSidenav"
      ></i>

      <router-link class="m-0 navbar-brand" to="/">
        <div class="logo-img navbar-brand-img h-100">
          <img :src="buddyimg" alt="">
          <span class="ms-2 fw-bold me-2">BUDDY</span>
        </div>
        <!-- <img
          :src="darkMode || sidebarType === 'bg-default' ? logoWhite : logo"
          class="navbar-brand-img h-100"
          alt="main_logo"
        /> -->
        <!-- <span class="ms-2 font-weight-bold me-2">BUDDY</span> -->
      </router-link>
    </div>

    <hr class="mt-0 horizontal dark" />

    <sidenav-list />
  </aside>
</template>
<style>
  .logo-img{
    /* width: 40px; */
    display: inline-flex;
    justify-content: center;
    align-items: center;
    /* height: 40px; */
    margin-left: 18%;
    margin-right: 10px;
    /* background: white; */
  }

  img{
    max-width: 50px;
    border-radius: 50%;
  }
  </style>
