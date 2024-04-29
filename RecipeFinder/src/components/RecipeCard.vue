<!-- <template>
    <div class="card" @click="emitRecipeId">
      <h4>{{ recipe.title }}</h4>
      <img :src="recipe.image" :alt="recipe.title" style="width: 100%;">
    </div>
  </template> -->
  
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
        </h5>
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
.custom-card img {
  width: 100%; /* Ensure the image is full width */
  height: auto; /* Maintain the aspect ratio */
  object-fit: cover; /* Cover the available area without losing the aspect ratio */
  border: solid .20rem white;
  border-radius: 10px;
}
  </style>
  