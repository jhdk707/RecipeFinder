<template>
  <fwb-navbar class="bg-yellow-400 text-black">
    <template #logo>
      <h1 class="mb-4 text-3xl font-extrabold tracking-tight leading-none text-black md:text-3l lg:text-4xl drop-shadow-lg">Ingredient I.Q</h1>
    </template>
    <template #default="{ isShowMenu }">
      <fwb-navbar-collapse :is-show-menu="isShowMenu" class="text-black">
        <fwb-navbar-link :style="{ color: isActive('/') ? 'white' : 'black' }" link="/" class="text-black hover:text-gray-400">
          Home
        </fwb-navbar-link>
        <fwb-navbar-link :style="{ color: isActive('/search') ? 'blue' : 'black' }" link="/search" class="text-black hover:text-gray-400">
          Search
        </fwb-navbar-link>
        <fwb-navbar-link :style="{ color: isActive('/about') ? 'blue' : 'black' }" link="/about" class="text-black hover:text-gray-400">
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
  console.log(`Current path: ${route.path}, Target path: ${path}`); // This will show the paths being compared
  return route.path === path;
}
</script>

<style scoped>

h1{
  color:white;
  text-shadow: 1px 1px 2px #000;
  margin: .25em;
}


/* Further emphasize hover states as well */
.fwb-navbar-link[aria-current="page"]:hover {
  color: darkblue; 
}
</style>




