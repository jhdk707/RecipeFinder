<template>
    <div class="modal">
      <button class="close" @click="$emit('closeModal')">Close</button>
      <div class="modal-content">
        <h2>{{ recipe.title }}</h2>
        <img :src="recipe.image" :alt="recipe.title">
        <!-- Ingredients List -->
        <h3>Ingredients:</h3>
        <ul>
          <li v-for="ingredient in recipe.extendedIngredients" :key="ingredient.id">
            {{ ingredient.amount }} {{ ingredient.unit }} {{ ingredient.name }}
          </li>
        </ul>
        <p>Preparation time: {{ recipe.readyInMinutes }} minutes</p>
        <a class="link" :href="recipe.sourceUrl" target="_blank">Read Full Recipe</a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      recipe: Object
    }
  }
  </script>
  
  <style>
  .modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    z-index: 1000;
    width: 80%;
    max-width: 600px;
    height: auto;
    overflow-y: auto;
    color: black;
  }
  
  .modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .modal-content img {
    width: 100%;
    max-width: 300px;
    height: auto;
    margin: 10px 0;
  }
  
  .modal-content ul {
    list-style-type: none;
    padding: 0;
  }
  
  .modal-content li {
    margin-bottom: 5px;
  }

  .close{
    color:red;
  }

  .link{
    color: blue;
  }
  </style>
  