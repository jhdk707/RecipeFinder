<template>
  <div class="modal">
    <button class="close inline-flex justify-center items-center py-1 px-5 text-sm font-semibold text-center text-white rounded-lg bg-red-700" @click="$emit('closeModal')">Close</button>
    <div class="modal-content">
      <h2>{{ recipe.title }}</h2>
      <img :src="recipe.image" :alt="recipe.title" loading="lazy">
      <h3 class="text-base custom-hover" v-if="recipe.extendedIngredients.length > 10" @click="toggleIngredients">
        <span>{{ showIngredients ? 'Hide' : 'Show' }} Ingredients </span>
      </h3>
      <ul v-show="showIngredients || recipe.extendedIngredients.length <= 10">
        <li v-for="ingredient in aggregatedIngredients" :key="ingredient.id">
          {{ ingredient.amount }} {{ ingredient.unit }} {{ ingredient.name }}
        </li>
      </ul>
      <p>Preparation time: {{ recipe.readyInMinutes }} minutes</p>
      <a class="link inline-flex justify-center items-center py-1 px-5 text-sm font-semibold text-center text-white rounded-lg bg-green-700" :href="recipe.sourceUrl" target="_blank">Read Full Recipe</a>
    </div>
  </div>
</template>



  
<script>
export default {
  props: {
  recipe: {
    type: Object,
    required: true,
    default: () => ({})
  }
},
  data() {
    return {
      showIngredients: false  // Controls the visibility of the ingredients list
    };
  },
  computed: {
    aggregatedIngredients() {
      const ingredientMap = new Map();  // Use a Map to track ingredients by name

      this.recipe.extendedIngredients.forEach((ingredient) => {
        const key = ingredient.name.toLowerCase().trim();  // Normalize the key to avoid case-sensitive duplicates
        if (ingredientMap.has(key)) {
          // If the ingredient is already in the map, add to its amount
          const existing = ingredientMap.get(key);
          existing.amount += parseFloat(ingredient.amount) || 0;  // Ensure the amount is a number, defaulting to 0 if NaN
          ingredientMap.set(key, existing);
        } else {
          // Otherwise, add the ingredient to the map
          ingredientMap.set(key, { 
            ...ingredient, 
            amount: parseFloat(ingredient.amount) || 0  // Ensure the initial amount is a number
          });
        }
      });

      // Convert the Map back to an array
      return Array.from(ingredientMap.values());
    }
  },
  methods: {
    toggleIngredients() {
      this.showIngredients = !this.showIngredients;  // Toggle visibility
    }
  },
  mounted() {
    // Preload the image as soon as the component mounts
    const img = new Image();
    img.src = this.recipe.image;
    img.onload = () => {
      console.log('Image preloaded successfully');
    };
    img.onerror = () => {
      console.error('Failed to preload image');
    };
  }
}
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
  