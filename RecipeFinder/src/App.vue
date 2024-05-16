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
  overflow: hidden; 
  height: 100vh;
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
  margin-top: 70px;
  margin-bottom: 10px;
  box-sizing: border-box;
  height: 100vh;
}

@media (max-width: 680px) {

  .headercontainer {
  position: fixed;
  width: 100%;
  z-index: 1000;
  background-color: #181818;
  }

  .viewcontainer {
  width: 100vw; 
  margin-top: 65px; 
  box-sizing: border-box; 
  height: 90vh;
  }

  .body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  margin: 0;
  padding: 0;
  overflow-y: auto;
  margin-bottom: 5px;
  }
}
</style>
