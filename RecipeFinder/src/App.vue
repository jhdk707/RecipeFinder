<script setup>
import { RouterView } from 'vue-router'
import HeaderBar from './components/HeaderBar.vue'
</script>

<template class="overflow-y-auto">
  <div class="body">
  <div class="headercontainer">
  <HeaderBar/>
  </div>
  <div class="viewcontainer">
  <RouterView />
  </div> 
</div> 
</template>

<style scoped>

.body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  margin: 0;
  padding: 0;
  overflow: hidden; /* Prevent scrolling on the body directly */
}

.headercontainer {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  background-color: #181818;
}

.viewcontainer {
  width: 100vw;
  overflow-y: auto;
  box-sizing: border-box;
}



@media (max-width: 680px) {

  .headercontainer {
  position: fixed;
  margin-top: 2em; 
  width: 100%;
  z-index: 1000;
  background-color: #181818;
  }

  .viewcontainer {
  width: 100vw; /* Adjusted to 100% of the viewport width for consistency */
  margin-top: 95px; 
  overflow-y: auto; /* Ensures scroll within this container only */
  height: calc(90vh - 20px); /* Subtract the header's height from the viewport height */
  box-sizing: border-box; /* Include padding in height calculation */
  }

  .body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  margin: 0;
  padding: 0;
  overflow: hidden; /* Prevent scrolling on the body directly */
  }
}
</style>
