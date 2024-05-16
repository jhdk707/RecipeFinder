<template>
  <div class="searchbody flex justify-start">
    <form @submit.prevent="searchRecipes" class="search-form">
      <fwb-input v-model="ingredients" type="text" class="inputform" placeholder="Enter ingredients on hand, separated by commas"></fwb-input>
      <fwb-button size="md" type="submit" class="searchbutton" color="green">Search Recipes</fwb-button>
    </form>
  <div class="searchcontainer">
    <div class="recipes-grid">
      <RecipeCard
        v-for="recipe in recipes"
        :key="recipe.id"
        :recipe="recipe"
        @selectRecipe="handleSelectRecipe"
      />
    </div>
    <!-- Modal Render -->
    <RecipeDetailsModal v-if="selectedRecipe" :recipe="selectedRecipe" @closeModal="selectedRecipe = null" />
  </div>
</div>
</template>
  
<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { FwbButton, FwbInput } from 'flowbite-vue';
import axios from 'axios';
import RecipeCard from '../components/RecipeCard.vue';
import RecipeDetailsModal from '../components/RecipeDetailsModal.vue';

const ingredients = ref('');
const recipes = ref([]);
const selectedRecipe = ref(null);

const saveSearch = () => {
  localStorage.setItem('savedIngredients', ingredients.value);
};

const loadSearch = () => {
  const savedIngredients = localStorage.getItem('savedIngredients');
  if (savedIngredients) {
    ingredients.value = savedIngredients;
    searchRecipes();
  }
};

const clearSearch = () => {
  console.log("Clearing search data from localStorage");
  localStorage.removeItem('savedIngredients');
};

const searchRecipes = async () => {
  try {
    // Initial search to find recipe IDs
    const searchOptions = {
      method: 'GET',
      url: 'https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/findByIngredients',
      params: {
        ingredients: ingredients.value,
        number: '30', // Adjust based on desired number of results
        ranking: '1',
        ignorePantry: 'true'
      },
      headers: {
        'X-RapidAPI-Key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',
        'X-RapidAPI-Host': 'spoonacular-recipe-food-nutrition-v1.p.rapidapi.com'
      }
    };

    // Fetch initial recipe IDs
    const searchResponse = await axios.request(searchOptions);
    const ids = searchResponse.data.map(recipe => recipe.id).join(',');

    // Fetch detailed information in bulk using the gathered IDs
    if (ids.length > 0) {
      const detailOptions = {
        method: 'GET',
        url: 'https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/informationBulk',
        params: { ids },  // Using the collected IDs
        headers: {
          'X-RapidAPI-Key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',
          'X-RapidAPI-Host': 'spoonacular-recipe-food-nutrition-v1.p.rapidapi.com'
        }
      };

      const detailResponse = await axios.request(detailOptions);
      recipes.value = detailResponse.data;  // This will now include all detailed information
    }
  } catch (error) {
    console.error('Error fetching recipes:', error);
  }
};

const handleSelectRecipe = (recipeId) => {
  selectedRecipe.value = recipes.value.find(recipe => recipe.id === recipeId);
};

onMounted(() => {
  loadSearch();
  searchRecipes(); 
  window.addEventListener('beforeunload', clearSearch);
});

onBeforeUnmount(() => {
  saveSearch();
  window.removeEventListener('beforeunload', clearSearch);
});
</script>


<script>
export default {
  components: {
    RecipeCard,
    RecipeDetailsModal
  },
  setup() {
    return {
      ingredients,
      recipes,
      selectedRecipe,
      searchRecipes,
    };
  }
};
</script>
  
<style>
.recipes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  width: 90%;
  max-width: 2300px; 
  height: 85vh;
  margin-top:50px;
  padding: 10px;
}

input {
  color:black;
}

.searchcontainer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 10px;
  overflow-y: auto; /* Enables scrolling only when content overflows */
  margin-bottom: 40px;
}

.search-form {
  width: 100%; 
  background-color: #181818;   
  padding: .5em;
  display: flex;
  gap: 5px; 
  position: fixed;
}

@media (min-width: 345px){
.inputform{
  width: 100%;
}

.searchbutton{
  width: 55%;
}

}
</style>