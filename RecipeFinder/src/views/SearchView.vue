<template>
    <div>
      <form @submit.prevent="searchRecipes">
        <input type="text" v-model="ingredients" placeholder="Enter ingredients separated by commas">
        <button type="submit">Search Recipes</button>
      </form>
      <div class="recipes-grid">
        <RecipeCard v-for="recipe in recipes" :key="recipe.id" :recipe="recipe" />
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import RecipeCard from '../components/RecipeCard.vue';
  
  export default {
    components: {
      RecipeCard
    },
    data() {
      return {
        ingredients: '',
        recipes: [],
        error: ''
      };
    },
    methods: {
      async searchRecipes() {
        const options = {
          method: 'GET',
          url: 'https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/findByIngredients',
          params: {
            ingredients: this.ingredients,
            ranking: '1',
            ignorePantry: 'true',
            number: '10'
          },
          headers: {
            'X-RapidAPI-Key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',
            'X-RapidAPI-Host': 'spoonacular-recipe-food-nutrition-v1.p.rapidapi.com'
          }
        };
  
        try {
          const response = await axios.request(options);
          this.recipes = response.data;
          this.error = '';  // Clear any previous errors
        } catch (error) {
          console.error(error);
          this.error = 'Failed to fetch recipes. Please check your API key and network connection.';
        }
      }
    }
  }
  </script>
  
  
  <style>
  .recipes-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
  }

    input{
    color:black;
  }
  </style>
  