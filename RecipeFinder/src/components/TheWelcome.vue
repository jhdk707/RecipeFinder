<script setup>
import WelcomeItem from './WelcomeItem.vue'
</script>

<template>
  <WelcomeItem>
    <template #heading>Search Recipe Finder</template>
    Head over to the "Search" tab to look for recipes based on ingredients that you have on hand! Each item will return of a list of needed ingredients & equipment before you view the recipe
  </WelcomeItem>


  <WelcomeItem>
    <template #heading>Support</template>
    This project is free to use! I just built it for fun. You are welcome to donate if you want to buy the dev some coffee or beer! 
  </WelcomeItem>
</template>
