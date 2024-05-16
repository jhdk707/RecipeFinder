    <template>
    <fwb-card
      :img-alt="recipe.title"
      :img-src="recipe.image"
      variant="image"
      @click="emitRecipeId"
      class="custom-card"
    >
      <div class="p-5">
        <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
          {{ recipe.title }}
          {{ recipe.properties }}
        </h5>
      </div>
      <div class="dietary-icons">
      <img v-if="recipe.vegan" src="@/components/icons/vegan_PNG25.png" alt="Vegan" />
      <img v-if="recipe.vegetarian" src="@/components/icons/vegetarian.jpg" alt="Vegetarian" />
      <img v-if="recipe.glutenFree" src="@/components/icons/glutenfree.jpg" alt="Gluten-Free" />
      <img v-if="recipe.dairyFree" src="@/components/icons/dairyfree.png" alt="Dairy-Free" />
      <img v-if="recipe.ketogenic" src="@/components/icons/ketologo.jpg" alt="Ketogenic" />
    </div>
    </fwb-card>
  </template>

    <script setup>
    // Import the necessary component from Flowbite-Vue
    import { FwbCard } from 'flowbite-vue';
    </script>

  <script>
  export default {
    props: {
      recipe: {
      type: Object,
      required: true
    }
    },
    methods: {
      emitRecipeId() {
        this.$emit('selectRecipe', this.recipe.id);
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
.custom-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Ensures that the content is spaced out and the icons stay at the bottom */
  height: 100%; /* Set the height to 100% to use the full height of the card */
}

.custom-card img {
  width: 100%; 
  height: auto; 
  object-fit: cover; 
  border: solid .20rem white;
  border-radius: 10px;
}

.dietary-icons {
  text-align: center; /* Center the icons horizontally */
  padding: 10px 0; /* Add some padding at the top and bottom for spacing */
}

.dietary-icons img {
  width: 48px;
  height: 48px;
  margin: 0 5px; /* Centering and providing equal horizontal space around icons */
  display: inline-block; /* Align icons in a line */
  vertical-align: middle; /* Align icons vertically in the middle */
}
  </style>
  