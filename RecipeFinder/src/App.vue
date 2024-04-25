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
  height: 100vh;
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
  height: 40px; /* Ensure this is the actual height of your header */
}

.viewcontainer {
  width: 100vw; /* Adjusted to 100% of the viewport width for consistency */
  margin-top: 300px; /* Should match the header's height */
  overflow-y: auto; /* Ensures scroll within this container only */
  height: calc(100vh - 40px); /* Subtract the header's height from the viewport height */
  box-sizing: border-box; /* Include padding in height calculation */
}



@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
