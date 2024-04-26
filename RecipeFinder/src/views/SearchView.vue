<template>
    <div class="searchcontainer">
      <form @submit.prevent="searchRecipes">
        <fwb-input v-model="ingredients" type="text" placeholder="Enter ingredients on hand, separated by commas"></fwb-input>
        <fwb-button size="md" type="submit">Search Recipes</fwb-button>
      </form>
      <div class="recipes-grid">
        <RecipeCard
          v-for="recipe in recipes"
          :key="recipe.id"
          :recipe="recipe"
          @selectRecipe="fetchRecipeDetails"
        />
      </div>
      <!-- Modal Render -->
      <RecipeDetailsModal v-if="selectedRecipe" :recipe="selectedRecipe" @closeModal="selectedRecipe = null" />
    </div>
  </template>
  
  <script setup>
  import { FwbButton, FwbInput } from 'flowbite-vue'
  </script>


  <script>
  import axios from 'axios';
  import RecipeCard from '../components/RecipeCard.vue';
  import RecipeDetailsModal from '../components/RecipeDetailsModal.vue';

  
  export default {
    components: {
      RecipeCard,
      RecipeDetailsModal
    },
    data() {
      return {
        ingredients: '',
        recipes: [],
        selectedRecipe: null
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
      },
      async fetchRecipeDetails(recipeId) {
        const options = {
          method: 'GET',
          url: `https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/${recipeId}/information`,
          headers: {
            'X-RapidAPI-Key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',
            'X-RapidAPI-Host': 'spoonacular-recipe-food-nutrition-v1.p.rapidapi.com'
          }
        };
        try {
          const response = await axios.request(options);
          this.selectedRecipe = response.data;
        } catch (error) {
          console.error(error);
        }
      }
    }
  }
</script>
  
<style>
.recipes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
  margin: 2em;
}

input {
  color:black;
}

.searchcontainer {
  margin-top: 2%;
  max-height: 50%;
  justify-content: center;
}

form{
  background-color: #181818;   
  padding: .5em;
  margin-left: 2em;
  max-width: 800px;
}
</style>