<template>
  <fwb-navbar class="bg-yellow-400 text-black">
    <template #logo>
      <h1 class="mb-4 text-3xl font-extrabold tracking-tight leading-none text-black md:text-3l lg:text-4xl drop-shadow-lg">Jesse's Recipe Finder</h1>
    </template>
    <template #default="{ isShowMenu }">
      <fwb-navbar-collapse :is-show-menu="isShowMenu" class="text-black">
        <fwb-navbar-link :is-active="isActive('/')" link="/" class="text-black hover:text-gray-900">
          Home
        </fwb-navbar-link>
        <fwb-navbar-link :is-active="isActive('/search')" link="/search" class="text-black hover:text-gray-700">
          Search
        </fwb-navbar-link>
        <fwb-navbar-link :is-active="isActive('/about')" link="/about" class="text-black hover:text-gray-700">
          About
        </fwb-navbar-link>
      </fwb-navbar-collapse>
    </template>
  </fwb-navbar>
</template>


<script setup>
import { FwbNavbar, FwbNavbarCollapse, FwbNavbarLink } from 'flowbite-vue';
import { useRoute } from 'vue-router';

const route = useRoute();

const isActive = (path) => {
  return route.path === path;
}
</script>

<style scoped>

h1{
  color:white;
  text-shadow: 1px 1px 2px #000;
}


</style>




