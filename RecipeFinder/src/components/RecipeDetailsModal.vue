<template>
  <div class="modal">
    <button
      class="close inline-flex justify-center items-center py-1 px-5 text-sm font-semibold text-center text-white rounded-lg bg-red-700"
      @click="$emit('closeModal')"
    >
      Close
    </button>
    <div class="modal-content">
      <h2>{{ recipe.title }}</h2>
      <img :src="recipe.image" :alt="recipe.title" loading="lazy" />
      <h3 class="text-base custom-hover" v-if="recipe.extendedIngredients.length > 10" @click="toggleIngredients">
        <span>{{ showIngredients ? 'Hide' : 'Show' }} Ingredients</span>
      </h3>
      <ul v-show="showIngredients || recipe.extendedIngredients.length <= 10">
        <li v-for="ingredient in aggregatedIngredients" :key="ingredient.id">
          {{ ingredient.amount }} {{ ingredient.unit }} {{ ingredient.name }}
        </li>
      </ul>
      <p>Preparation time: {{ recipe.readyInMinutes }} minutes</p>
      <h3>Nutrition Information:</h3>
      <ul v-if="nutrition">
        <li v-for="(value, key) in nutrition.combinedTotals" :key="key">
          {{ key }}: {{ value }}
        </li>
      </ul>
      <p v-else>Loading nutrition information...</p>
      <a
        class="link inline-flex justify-center items-center py-1 px-5 text-sm font-semibold text-center text-white rounded-lg bg-green-700"
        :href="recipe.sourceUrl"
        target="_blank"
      >
        Read Full Recipe
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recipe: {
      type: Object,
      required: true,
      default: () => ({}),
    },
  },
  data() {
    return {
      showIngredients: false,
      nutrition: null, // Store nutrition data
    };
  },
  computed: {
    aggregatedIngredients() {
      const ingredientMap = new Map();

      this.recipe.extendedIngredients.forEach((ingredient) => {
        const key = ingredient.name.toLowerCase().trim();
        if (ingredientMap.has(key)) {
          const existing = ingredientMap.get(key);
          existing.amount += parseFloat(ingredient.amount) || 0;
          ingredientMap.set(key, existing);
        } else {
          ingredientMap.set(key, {
            ...ingredient,
            amount: parseFloat(ingredient.amount) || 0,
          });
        }
      });

      return Array.from(ingredientMap.values());
    },
  },
  methods: {
    toggleIngredients() {
      this.showIngredients = !this.showIngredients;
    },
    async fetchNutrition() {
  const url = `https://spoonacular-recipe-food-nutrition-v1.p.rapidapi.com/recipes/${this.recipe.id}/nutritionWidget.json`;
  const options = {
    method: 'GET',
    headers: {
      'x-rapidapi-key': '16f87e2059mshe937410fce7f782p1d1cc9jsnae5dd54150f4',
      'x-rapidapi-host': 'spoonacular-recipe-food-nutrition-v1.p.rapidapi.com',
    },
  };

  try {
    const response = await fetch(url, options);
    const result = await response.json();
    console.log('API Response:', result);  // Log the response to debug

    this.nutrition = {
      combinedTotals: {
        calories: result.calories,
        carbs: result.carbs,
        fat: result.fat,
        protein: result.protein
      },
    };
  } catch (error) {
    console.error('Failed to fetch nutrition information:', error);
    this.nutrition = { error: 'Unable to load nutrition data.' };
  }
}
  },
  mounted() {
    this.fetchNutrition(); // Fetch nutrition data when the component is mounted
  },
};
</script>



  
<style>
  .modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(245, 245, 245, 0.949);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  width: 90%;
  max-width: 600px;
  max-height: 80vh; 
  overflow-y: auto; 
  color: black;
  border: solid .1em rgb(255, 255, 255);
  box-shadow: 2px 2px 2px;
  }

  .modal-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  }

  .modal-content img {
  width: 100%;
  max-width: 400px;
  height: auto;
  margin: 10px 0;
  border-radius: 10px;
  border: solid .2em rgb(255, 255, 255);
  }

  .modal-content ul {
  list-style-type: none;
  padding: 0;
  max-height: 300px; /* Maximum height for the ingredients list */
  overflow-y: auto; /* Enable vertical scrolling */
  width: 100%; /* Ensure the list uses the full width of the modal content */
  background: rgba(255,255,255,0.7);
  padding: .5em;
  border-radius: 10px;
  border: solid .1em rgb(255, 255, 255);
  }

  .modal-content li {
  margin-bottom: 5px;
  }

  h2{
    font-weight: 700;
    font-size:large;
    margin-top: 3px;
  }

  .custom-hover:hover {
    font-weight: bold; /* Ensure this is not getting overridden */
  }


  h3 {
    cursor: pointer; 
    user-select: none; 
    color: green; 
    margin-bottom: 5px;
  }

  h3 span {
  display: inline-block;
  transition: transform 0.3s ease;
  }

  h3 span.rotate {
  transform: rotate(90deg); 
  }

  p {
    margin-bottom: 5px;
  }

</style>
  