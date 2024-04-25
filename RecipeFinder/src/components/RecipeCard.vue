<template>
    <div class="card" @click="emitRecipeId">
      <h4>{{ recipe.title }}</h4>
      <img :src="recipe.image" :alt="recipe.title" style="width: 100%;">
    </div>
  </template>
  
  <script>
  export default {
    props: {
      recipe: Object
    },
    methods: {
      emitRecipeId() {
        this.$emit('selectRecipe', this.recipe.id);
      }
    }
  }
  </script>
  
  
  <style>
  .card {
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    padding: 10px;
    border-radius: 5px;
    background-color: antiquewhite;
    color: black;
  }

  </style>
  